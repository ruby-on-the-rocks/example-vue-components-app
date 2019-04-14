<template>
  <div class="home">
    <div>
      <multiselect v-model="value2" v-bind:options="options" v-bind:multiple="true"></multiselect>
    </div>

    <label>{{ selectedEvent }}</label>
    <vue-instant
      :suggestOnAllWords="true"
      :suggestion-attribute="suggestionAttribute"
      v-model="value"
      :disabled="false"
      @input="changed"
      @click-input="clickInput"
      @click-button="clickButton"
      @selected="selected"
      @enter="enter"
      @key-up="keyUp"
      @key-down="keyDown"
      @key-right="keyRight"
      @clear="clear"
      @escape="escape"
      :show-autocomplete="true"
      :autofocus="false"
      :suggestions="suggestions"
      name="customName"
      placeholder="custom placeholder"
      type="google"
    ></vue-instant>

    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import Multiselect from "vue-multiselect";

import Vue from "vue";
import "vue-instant/dist/vue-instant.css";
import VueInstant from "vue-instant";
import axios from "axios";
Vue.use(VueInstant);

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
      value2: [],
      options: ["list", "of", "options"],

      value: "",
      suggestionAttribute: "original_title",
      suggestions: [],
      selectedEvent: ""
    };
  },
  methods: {
    clickInput() {
      this.selectedEvent = "click input";
    },
    clickButton() {
      this.selectedEvent = "click button";
    },
    selected() {
      this.selectedEvent = "selection changed";
    },
    enter() {
      this.selectedEvent = "enter";
    },
    keyUp: function() {
      this.selectedEvent = "keyup pressed";
    },
    keyDown: function() {
      this.selectedEvent = "keyDown pressed";
    },
    keyRight: function() {
      this.selectedEvent = "keyRight pressed";
    },
    clear: function() {
      this.selectedEvent = "clear input";
    },
    escape: function() {
      this.selectedEvent = "escape";
    },
    changed: function() {
      var that = this;
      this.suggestions = [];
      axios
        .get("https://api.themoviedb.org/3/search/movie?api_key=342d3061b70d2747a1e159ae9a7e9a36&query=" + this.value)
        .then(function(response) {
          response.data.results.forEach(function(a) {
            that.suggestions.push(a);
          });
        });
    }
  }
};
</script>
