<template>
  <div id="app">
    <VueChild title="TODO List" />
  </div>
</template>

<script>
import VueChild from "./components/VueChild.vue";

export default {
  name: "App",
  components: {
    VueChild
  }
};
</script>
