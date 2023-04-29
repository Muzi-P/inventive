<template>
  <footer>
    <div class="container">
      <div class="row">
        <div class="col-lg-4">
          <div class="item md-mb50">
            <div class="title">
              <h5>Contact Us</h5>
            </div>
            <ul>
              <li>
                <span class="icon pe-7s-map-marker" />
                <div class="cont">
                  <h6>Official Address</h6>
                  <p>
                    {{ appData.address.state }} , {{ appData.address.country }}
                  </p>
                </div>
              </li>
              <li>
                <span class="icon pe-7s-mail" />
                <div class="cont">
                  <h6>Email Us</h6>
                  <p>{{ appData.email }}</p>
                </div>
              </li>
              <li>
                <span class="icon pe-7s-call" />
                <div class="cont">
                  <h6>Call Us</h6>
                  <p>{{ appData.phone }}</p>
                </div>
              </li>
            </ul>
          </div>
        </div>
        <div class="col-lg-4">
          <div class="item md-mb50">
            <div class="title">
              <h5>Recent News</h5>
            </div>
            <ul>
              <li
                v-for="item in appData.footerNews"
                :key="item.id"
              >
                <div class="img">
                  <img
                    style="width: 4.5rem;height: 4rem;"
                    :src="item.img"
                    alt=""
                  >
                </div>
                <div class="sm-post">
                  <p>{{ item.title }}</p>
                  <span class="date">{{ item.date }}</span>
                </div>
              </li>
            </ul>
          </div>
        </div>
        <div class="col-lg-4">
          <div class="item">
            <div class="logo">
              <img
                :src="appData.lightLogo"
                alt=""
              >
            </div>
            <div class="social">
              <NuxtLink to="#0">
                <i class="fab fa-facebook-f" />
              </NuxtLink>
              <NuxtLink to="#0">
                <i class="fab fa-twitter" />
              </NuxtLink>
              <NuxtLink to="#0">
                <i class="fab fa-instagram" />
              </NuxtLink>
              <NuxtLink to="#0">
                <i class="fab fa-youtube" />
              </NuxtLink>
            </div>
            <div class="copy-right">
              <p>
                @ {{ new Date().getFullYear() }} ,{{ appData.footerText }}
                <a
                  v-for="author in appData.themeAuthors"
                  :key="author.name"
                  :href="author.href"
                >{{ author.name }}</a>.
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
import appData from "../../data/app.json";

export default {
  name: "Footer",
  data() {
    return {
      appData
    };
  }
};
</script>
