<template>
  <div class="home">
    <div>
      <multiselect v-model="value" v-bind:options="options" v-bind:multiple="true"></multiselect>
    </div>

    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import Multiselect from "vue-multiselect";

// register globally
// Vue.component("multiselect", Multiselect);

export default {
  name: "home",
  components: {
    HelloWorld,
    Multiselect
  },
  data() {
    return {
      value: [],
      options: ["list", "of", "options"]
    };
  }
};
</script>
