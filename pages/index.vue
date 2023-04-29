<template>
  <div>
    <Navbar ref="navbar" theme="dark" />
    <Home2-Light-Header />
    <Home3-Light-Services />
    <Home3-Light-Works />
    <Home1-Light-About />
    <!-- <Home3-Light-Numbers /> -->
    <Home3-Light-Testimonials />
    <Home2-Light-News />
    <Footer />
  </div>
</template>

<script>
export default {
  name: 'Home3-Light',
  layout: "light",
  head() {
    return {
      titleTemplate: "%s",
    }
  },
  mounted() {
    document.body.classList.remove('index2');
    document.body.classList.remove('index3');
    document.body.classList.remove('index4');

    var navbar = this.$refs.navbar.$el;

    if (window.pageYOffset > 300) navbar.classList.add("nav-scroll");
    else navbar.classList.remove("nav-scroll");

    window.addEventListener("scroll", () => {
      if (window.pageYOffset > 300) navbar.classList.add("nav-scroll");
      else navbar.classList.remove("nav-scroll");
    });
  }
}
</script>