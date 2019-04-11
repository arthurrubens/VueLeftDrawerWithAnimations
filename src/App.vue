<template>
  <div id="app">
    <Drawer :user="user"/>
  </div>
</template>

<script>
import Drawer from "./components/Drawer.vue";

export default {
  name: "app",
  data: function() {
    return {
      user: {
        firstName: "Arthur",
        lastName: "Rubens",
        avatar: "./img/ArthurRubensAvatarRound.png"
      }
    };
  },

  components: {
    Drawer
  }
};
</script>

<style scoped>
</style>
