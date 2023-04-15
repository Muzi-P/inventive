<template>
  <section class="contact">
    <div class="container-fluid">
      <div class="row justify-content-center">
        <div class="col-lg-6 form">
          <BookVenueForm />
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import contactData from "../../data/contact.json";

export default {
  name: "Contact",
  data() {
    return {
      contactData
    }
  }
}
</script>
