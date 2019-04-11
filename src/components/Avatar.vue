<template>
  <div class="avatarWrapper">
    <img :src="src" class="avatarImage" :style="{ transform: 'rotate(' + avatarRotateDeg + 'deg)' }">
  </div>
</template>

<script>
import { clearInterval } from 'timers';

export default {
  name: 'Avatar',
  props: {
    src: String
  },
  components: {},
  data: function() {
    return {
      avatarRotateDeg: 0,
    }
  },
  methods: {
    doRotateAvatar: function(avatarRotateDegStep) {
      var me = this,
          maxRotationDeg = 360,
          avatarRotateIntervalId = setInterval(function() {
              if(Math.abs(me.avatarRotateDeg) < maxRotationDeg ) {
                me.avatarRotateDeg = me.avatarRotateDeg + avatarRotateDegStep;
              } else {
                window.clearInterval(avatarRotateIntervalId);
                me.avatarRotateDeg = 0;
              }
          }, 1);
    }
  }
}
</script>

<style scoped>
.avatarWrapper {
    width: 100%;
    height: auto;
}

.avatarImage {
    display: block;
    max-width: 80%;
    height: inherit;
    margin: 0 auto 5px auto;
}

</style>
