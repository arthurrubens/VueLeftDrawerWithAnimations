<template>
  <div class="drawerItemWrapper">
    <a
      :href="'#' + text"
      @mouseover="doRotateIcon(5)"
      @mouseout="doRotateIcon(-5)"
      @click="onClick"
    >
      <i :class="['fa', 'pageIcon', icon, size]" :style="iconInlineStyle" aria-hidden="true"></i>
      <span :style="{'display': displayText}" class="pageTitle">{{text}}</span>
    </a>
  </div>
</template>

<script>
export default {
  name: "DrawerItem",
  props: {
    icon: String,
    text: String,
    displayText: String,
    size: String
  },
  data: function() {
    return {
      iconInlineStyle: {
        transform: "rotate(0deg)"
      },
      iconRotateDeg: 0
    };
  },
  methods: {
    doRotateIcon: function(iconRotateDegStep) {
      var me = this,
        maxRotationDeg = 360,
        rotateDeg = 0,
        avatarRotateIntervalId = setInterval(function() {
          if (Math.abs(rotateDeg) < maxRotationDeg) {
            rotateDeg += iconRotateDegStep;
          } else {
            window.clearInterval(avatarRotateIntervalId);
            rotateDeg = 0;
          }
          me.iconInlineStyle.transform = "rotate(" + rotateDeg + "deg)";
        }, 1);
    },
    onClick: function() {
      this.$emit("click", this.text);
    }
  },
  watch: {
    size: function(newVal, oldVal) {
      this.doRotateIcon(5);
    }
  }
};
</script>

<style scoped>
.drawerItemWrapper {
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  width: 100%;
  height: auto;
  margin: 0 0 5px 5px;
  padding: 5px;
  opacity: 0.5;
}

.pageIcon {
  margin-right: 10px;
}
</style>