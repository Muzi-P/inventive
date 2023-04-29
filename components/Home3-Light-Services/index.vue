 <template>
  <section class="services section-padding bg-gray"  id='contact'>
    <div class="container">
      <div class="section-head text-center">
        <div class="row justify-content-center">
          <div class="col-lg-6 col-md-8 col-sm-10">
            <h6 class="custom-font wow fadeInDown" data-wow-delay=".3s">Best Features</h6>
            <h4 class="playfont wow flipInX" data-wow-delay=".5s">Our Services</h4>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-lg-4 services item" v-for="service, idx in services" :key="idx">
          <div class="item-bx bg-img wow fadeInUp" :data-wow-delay="`${0.3 + idx * 0.2}s`" :style="`background-image:url('${service.image}')`">
            <span :class="`icon flaticon-${service.icon}`"></span>
            <h6 class="mb-20">{{ service.title }}</h6>
            <span v-if="service.truncated">
              <span v-if="!service.expanded">
                <p class="justify-content"  @click="handleExpand">{{ handleDescription(service) }} <span class="read-more" @click="handleExpand(service)">Read more</span> </p>
              </span>
              <span v-else>
                <p class="justify-content"  @click="handleExpand">{{ service.description}} <span class="read-more" @click="handleExpand(service)">Read less</span> </p>
              </span>
            </span>
            <span v-else>
              <p class="justify-content ">{{ handleDescription(service) }}</p>
            </span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Home3LightServicesData from "../../data/home3-light-services.json";

export default {
  name: "Home3-Light-Services",
  data() {
    return {
      services: [],
      expanded: false
    }
  },
  mounted() {
    let formattedServices = Home3LightServicesData.map(service => {
        service['truncated'] = service.description.length > 300
        service['expanded'] = false
        return service
      })
    this.services = formattedServices
  },
  methods: {
    handleDescription (service) {
      return service.description.length > 300 ? `${service.description.slice(0, 300)} ...` : service.description
    },
    handleExpand (service) {
      let updatedServices = [...this.services]

      updatedServices.forEach(s => {
        if (s.id == service.id) {
          s.expanded = !service.expanded
        }
      })

      this.services = updatedServices
    },
  },
}
</script>

<style scoped>
.read-more {
  color: #c5a47e;
  cursor: pointer;
}
</style>
