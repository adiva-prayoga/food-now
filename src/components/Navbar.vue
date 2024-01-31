<script>
import { ref } from "vue";
import Hero from "./Hero.vue";

export default {
  name: "Navbar",
  components: {
    Hero,
  },
  setup() {
    const isOpen = ref(false);

    const toggleMenu = () => {
      isOpen.value = !isOpen.value;
      document.body.classList.toggle("no-scroll", isOpen.value);
    };

    return {
      isOpen,
      toggleMenu,
    };
  },
};
</script>

<template>
  <nav v-if="!isOpen" class="navbar container">
    <div class="navbar--logo">
      <img src="/assets/logo.svg" alt="" />
    </div>

    <ul class="navbar--menu">
      <li>Home</li>
      <li class="navbar--menu--active">Order</li>
      <li>About</li>
      <li>Blog</li>
      <li>Contact us</li>
    </ul>

    <div class="navbar--action">
      <button class="button button--login">Login</button>
      <button class="button button--register">Register</button>
    </div>
  </nav>

  <nav
    class="navbar-mobile"
    :style="{
      transform: isOpen ? 'translateX(0)' : 'translateX(-100%)',
      transition: 'transform 0.35s ease-in-out',
    }"
  >
    <ul class="navbar-mobile--menu">
      <li>Home</li>
      <li class="navbar-mobile--menu--active">Order</li>
      <li>About</li>
      <li>Blog</li>
      <li>Contact us</li>
      <li class="button button--login-mobile">Login</li>
      <li class="button button--register-mobile">Register</li>
    </ul>
  </nav>

  <div @click="toggleMenu" class="navbar--hamburger">
    <div class="navbar--hamburger--wrapper">
      <div class="navbar--hamburger--wrapper--bar"></div>
      <div class="navbar--hamburger--wrapper--bar"></div>
    </div>
  </div>

  <Hero />
</template>
