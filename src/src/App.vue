<template>
  <div id="app">
    <the-wysiwyg />
  </div>
</template>

<script>
import TheWysiwyg from "./components/TheWysiwyg.vue";

export default {
  name: "App",
  components: {
    TheWysiwyg,
  },
};
</script>

<style lang="scss">
#app {
  height: 100%;
  width: 100%;
}
</style>
