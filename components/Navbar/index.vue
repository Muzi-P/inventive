<template>
  <nav :ref="nr" class="navbar navbar-expand-lg">
    <div class="container">
      <!-- Logo -->
      <NuxtLink to="/" class="logo">
        <img ref="lr" src="/img/logo-light.png"  alt="logo" v-if="showLogo !== false" style="width: 120%"/>
      </NuxtLink>

      <button
        @click="handleMobileDropdown"
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="icon-bar">
          <i class="fas fa-bars"></i>
        </span>
      </button>

      <!-- navbar links -->
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav ml-auto">
           <li class="nav-item">
            <NuxtLink class="nav-link" to="/">Home</NuxtLink>
          </li>
          <li class="nav-item">
            <NuxtLink class="nav-link" :to="{ path: '/',hash:'#contact'}">About</NuxtLink>
          </li>
          <li class="nav-item">
            <NuxtLink class="nav-link" to="/work-with-us">Work With Us</NuxtLink>
          </li>
          <li class="nav-item">
            <NuxtLink class="nav-link" :to="{ path: '/',hash:'#blog'}">Blog</NuxtLink>
          </li>
          <li class="nav-item">
            <NuxtLink class="nav-link" to="/contact">Contact</NuxtLink>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import getSiblings from "../../common/getSiblings";

export default {
  name: 'Navbar',
  props: ["lr", "theme", "nr", "showLogo"],
  methods: {
    handleDropdown: (e) => {
      getSiblings(e.target.parentElement).filter((item) => item.classList.contains("show")).map((item) => {
        item.classList.remove("show");
        if (item.childNodes[0]) {
          item.childNodes[0].setAttribute("aria-expanded", false);
        }
        if (item.childNodes[2]) {
          item.childNodes[2].classList.remove("show");
        }
      });

      e.target.setAttribute("aria-expanded", true);

      if (e.target.parentElement) {
        e.target.parentElement.classList.toggle("show");
        let dropdownMenu = e.target.parentElement.childNodes[2];
        if (dropdownMenu) {
          dropdownMenu.classList.toggle("show");
        }
      }
    },
    handleMobileDropdown: (e) => {
      document.getElementById("navbarSupportedContent").classList.toggle("show-with-trans");
    },
  }
}
</script>