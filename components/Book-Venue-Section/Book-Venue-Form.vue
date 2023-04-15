<template>
  <form
    id="book-venue-form"
    name="book-venue"
    action="contact.php"
    method="POST"
    data-netlify="true"
    netlify-honeybot="bot-field"
    class="needs-validation"
    novalidate
    @submit.prevent="onSubmit"
  >
    <input
      type="hidden"
      name="form-name"
      value="form-value"
    >
    <div class="controls">
      <div class="form-row">
        <div class="form-group col-md-6">
          <label for="form_name">Name</label>
          <input
            id="form_name"
            v-model="contactData.name"
            type="text"
            name="name"
            placeholder="Name"
            required="required"
          >
        </div>
        <div class="form-group col-md-6">
          <label for="form_surname">Surname</label>
          <input
            id="form_surname"
            v-model="contactData.surname"
            type="text"
            name="surname"
            placeholder="Surname"
            required="required"
          >
        </div>
      </div>
      <div class="form-row">
        <div class="form-group col-md-6 ">
          <label for="form_email">Email</label>
          <input
            id="form_email"
            v-model="contactData.email"
            type="email"
            name="email"
            placeholder="Email"
            required="required"
          >
        </div>
        <div class="form-group col-md-6 ">
          <label for="phone_number">Phone Number</label>
          <input
            id="phone_number"
            v-model="contactData.phoneNumber"
            type="number"
            name="phoneNumber"
            placeholder="Phone Number"
            required="required"
          >
        </div>
      </div>
      <div class="form-row">
        <div class="form-group col-md-6  d-flex flex-column">
          <label for="form_event_type">Event Type</label>
          <el-select
            v-model="contactData.eventType"
            placeholder="Select"
            required="required"
          >
            <el-option
              v-for="item in eventOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            />
          </el-select>
        </div>
        <div class="form-group col-md-6 d-flex flex-column">
          <label for="event_date">Event Date</label>
          <el-date-picker
            v-model="contactData.eventDate"
            format="dd MMMM yyyy"
            value-format="yyyy-MM-dd"
            type="date"
            required="required"
          />
        </div>
      </div>
      <div class="form-group">
        <label for="form_message">Message</label>
        <textarea
          id="form_message"
          v-model="contactData.message"
          name="message"
          placeholder="Message"
          rows="4"
          required="required"
        />
      </div>
      <div class="d-flex flex-row align-content-center flex-wrap">
        <div>
          <button
            type="submit"
            class="btn-curve btn-color btn-send-message"
            @click="onSubmit"
          >
            <span>Send Message</span>
          </button>
        </div>
        <div
          v-if="errMessage"
          class="form-error-messages ml-2 mt-3"
        >
          {{ errMessage }}
        </div>
      </div>
    </div>
    <!-- added for netlify form submissions, not visible in ui -->
    <div style="position: absolute;z-index: -1;top: 0; opacity: 0">
      <input
        v-model="subject"
        name="subject"
      >
    </div>
    <!-- end -->
  </form>
</template>

<script>
export default {
  name: "ContactForm",
  data() {
    return {
      contactData: {
        name: "",
        surname: "",
        email: "",
        message: "",
        phoneNumber: "",
        eventDate: null,
        eventType: "",
        subject: "This is a test subject"
      },
      eventOptions: [
        {
          label: "Corporate Event",
          value: "corporateEvent"
        },
        {
          label: "Social Event",
          value: "socialEvent"
        },
        {
          label: "Photo/Film Shoot",
          value: "photoShoot"
        },
        {
          label: "Wedding",
          value: "wedding"
        },
        {
          label: "Team Outing",
          value: "teamOuting"
        },
        {
          label: "Engagement Party",
          value: "engagementParty"
        },
        {
          label: "Bridal Shower",
          value: "bridalShower"
        },
        {
          label: "Meeting",
          value: "meeting"
        },
        {
          label: "Baby Shower",
          value: "babyShower"
        },
        {
          label: "Birthday Party",
          value: "birthdayParty"
        },
        {
          label: "Holiday Party",
          value: "holidayParty"
        },
        {
          label: "Other",
          value: "Other"
        }
      ],
      errMessage: ""
    };
  },
  computed: {
    subject() {
      return `Mone Reve Event Booked For ${this.contactData.eventDate}:  ${this.contactData.name} ${this.contactData.surname}`;
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();

      if (!this.validateForm(this.contactData)) return;

      this.errMessage = "";

      this.contactData.subject = this.subject;
      fetch("/", {
        method: "post",
        headers: { "Content-Type": "application/x-www-form-urlencoded" },
        body: this.encode({
          "form-name": "book-venue",
          ...this.contactData
        })
      }).then(() => {
        this.contactData = {};
        this.sendMessage();
      });
    },
    validateForm(contactData) {
      const allFieldsValid = Object.keys(contactData).every(
        key => contactData[key]
      );
      if (!allFieldsValid) {
        this.errMessage = "Please fill in all fields";
        return false;
      }

      if (
        !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i.test(contactData.email)
      ) {
        this.errMessage = "Email address is invalid";
        return false;
      }
      return true;
    },
    encode(data) {
      return Object.keys(data)
        .map(
          key => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`
        )
        .join("&");
    },
    sendMessage() {
      this.$swal({
        title: "Reservation request sent",
        text: "Our team will be in touch with you",
        icon: "success",
        confirmButtonText: "Ok"
      }).then(result => {
        if (result.value) {
          this.$router.push({
            path: "/"
          });
        }
      });
    }
  }
};
</script>
