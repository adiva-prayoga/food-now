<script>
export default {
  name: "Footer",
  data() {
    return {
      navigationItems: ["Home", "Order", "About", "Blog"],
      accountItems: ["Contact", "Login", "Register"],
      locationAddress:
        "Jl. Raya Kerobokan Br Taman, Kuta No.98, Kerobokan Kelod, Kec. Kuta Utara, Kabupaten Badung, Bali 80361",
      copyrightText:
        "Copyright © 2022 Foodnow. All Rights Reserved. Powered by PT. Timedoor Indonesia. | Privacy Policy",
      privacyPolicyText:
        "This site is protected by reCAPTCHA and the Google Privacy Policy and Terms of Service apply.",
    };
  },
};
</script>

<template>
  <footer class="footer container">
    <div class="footer--content">
      <div class="footer--content--logo">
        <img src="/assets/logo-alt.svg" alt="" />
        <div class="footer--content--logo--social">
          <h2>Find Us:</h2>
          <ul>
            <li>
              <img src="/assets/facebook.svg" alt="" />
            </li>
            <li>
              <img src="/assets/instagram.svg" alt="" />
            </li>
            <li>
              <img src="/assets/youtube.svg" alt="" />
            </li>
          </ul>
        </div>
      </div>
      <div class="footer--content--navigation">
        <h2>Navigation</h2>
        <div class="footer--content--navigation--list">
          <ul>
            <li v-for="item in navigationItems" :key="item">{{ item }}</li>
          </ul>
          <ul>
            <li v-for="item in accountItems" :key="item">{{ item }}</li>
          </ul>
        </div>
      </div>
      <div class="footer--content--contact">
        <h2>Contact</h2>
        <ul>
          <li>
            <span><img src="/assets/mail.svg" alt="" /></span>Food.now@mail.com
          </li>
          <li>
            <span><img src="/assets/phone.svg" alt="" /></span>+62848477102943
          </li>
          <li>
            <span><img src="/assets/whatsapp.svg" alt="" /></span>+628184938494
          </li>
        </ul>
      </div>
      <div class="footer--content--location">
        <h2>Location</h2>
        <div class="footer--content--location--address">
          <h3>
            <span> <img src="/assets/location.svg" alt="" /> </span>Kerobokan
          </h3>
          <p>{{ locationAddress }}</p>
        </div>
      </div>
    </div>
    <div class="footer--copyright">
      <h3>{{ copyrightText }}</h3>
      <p>{{ privacyPolicyText }}</p>
    </div>
  </footer>
</template>
