<template>
  <div class="content">
    <router-view/>
  </div>
</template>

<script>
import { mapActions } from "vuex";

export default {
  name: "app",
  methods: {
    ...mapActions({
      getData: "getData",
      initializeCart: "cart/initializeCart"
    })
  },
  created() {
    this.getData();
    this.initializeCart(this.$store);
  }
};
</script>

<style>
.content {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  max-width: 1000px;
}
</style>
