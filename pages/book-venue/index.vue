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
  name: 'BookVenue',
  layout: "dark",
  head() {
    return {
      titleTemplate: "%s - Book Venue",
    }
  },
  data() {
    return {
      title: "Book Our Venue",
      fullPath: [
        { title: 'Book Our Venue', link: "/book-venue" }
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