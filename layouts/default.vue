<template>
  <div>
    <app-nav />
    <main>
      <nuxt />
    </main>
    <app-footer />
  </div>
</template>

<script>
import AppFooter from "~/components/AppFooter.vue";
import AppNav from "~/components/AppNav.vue";
import { mapGetters } from "vuex";

export default {
  components: {
    AppFooter,
    AppNav
  },
  computed: {
    ...mapGetters(["cartTotal"])
  },
  mounted() {
    window.nudgify = {data: {"cart":{"amount":this.cartTotal,"currency":"USD"}}};
    
    (function(w){
        var k="nudgify",n=w[k]||(w[k]={});
        n.uuid="68ed61a2-868d-466a-9e92-dc55fd931ff0";
        var d=document,s=d.createElement("script");
        s.src="https://pixel-rc.nudgify.com/pixel.js";
        s.async=1;
        s.charset="utf-8";
        d.getElementsByTagName("head")[0].appendChild(s)
    })(window);
    
    window.addEventListener('cart-updated', (event) => {
      if (window.nudgify && window.nudgify.cart) {
        window.nudgify.cart(event.detail)
      }
    })
  }
};
</script>

<style scoped>
body {
  border: 10px solid #ccc;
  min-height: 100vh;
  font-family: "Montserrat", -apple-system, BlinkMacSystemFont, "Segoe UI",
    Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 16px;
  line-height: 1.4;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

main {
  padding: 0;
  width: 95vw;
  margin-left: 2vw;
}

@media screen and (min-width: 1000px) {
  main {
    padding: 40px;
    width: 80vw;
    margin-left: 7vw;
  }
}
</style>
