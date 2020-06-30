<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <TakayaZone msg="Welcome to Your Vue.js App" greet="HELLO!!" />
  </div>
</template>

<script>
// @ is an alias to /src
import TakayaZone from "@/components/TakayaZone.vue";

export default {
  name: "Home",
  components: {
    TakayaZone
  }
};
</script>
