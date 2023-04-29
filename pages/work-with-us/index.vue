<template>
  <div>
    <Navbar ref="navbar" />
    <Header2 bg="/img/slid/n/01.jpg" :title="title" :fullPath="fullPath" />
    <Book-Event-Intro />
    <Book-Venue-Section />
    <Footer />
  </div>
</template>

<script>
export default {
  name: 'WorkWithUs',
  layout: "dark",
  head() {
    return {
      titleTemplate: "%s - Work With Us",
    }
  },
  data() {
    return {
      title: "Work With Us",
      fullPath: [
        { title: 'Work With Us', link: "/work-with-us" }
      ]
    }
  },
  mounted() {
    document.body.classList.add('index3');
    document.body.classList.remove('index2');
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