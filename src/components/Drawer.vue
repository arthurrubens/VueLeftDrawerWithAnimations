<template>
  <div class="wrapper" :style="{ width: drawerWidth + 'px' }">
    <a href="#"
      v-on:click="onCollapseClick"
      class="collapseButton"
      :style="{'display': displayCollapseButton}"
    >
        <span class="fa fa-angle-double-left fa-2x" aria-hidden="true"/>
    </a>
    <a href="#"
      v-on:click="onExpandClick"
      class="expandButton"
      :style="{'display': displayExpandButton}"
    >
      <span class="fa fa-angle-double-right fa-2x" aria-hidden="true"/>
    </a>
    <Avatar :src="user.avatar" ref="avatar"/>
    <div class="userName">
      <span
        :style="{'display': displayUserName}"
      >
        {{user.firstName}} {{user.lastName}}
      </span>
    </div>
    <div class="menuWrapper">
      <div class="menuContainer">
        <DrawerItem icon="fa-calendar" text="Calender" :displayText="drawerItemDisplayText" :size="drawerItemIconSize"/>
        <DrawerItem icon="fa-bank" text="Bank" :displayText="drawerItemDisplayText" :size="drawerItemIconSize"/>
        <DrawerItem icon="fa-map-o" text="Map" :displayText="drawerItemDisplayText" :size="drawerItemIconSize"/>
        <DrawerItem icon="fa-graduation-cap" text="University" :displayText="drawerItemDisplayText" :size="drawerItemIconSize"/>
        <DrawerItem icon="fa-life-ring" text="Support" :displayText="drawerItemDisplayText" :size="drawerItemIconSize"/>
        <DrawerItem icon="fa-calendar" text="Calender" :displayText="drawerItemDisplayText" :size="drawerItemIconSize"/>
      </div>
    </div>
  </div>
</template>

<script>
import { clearInterval } from 'timers';
import DrawerItem from './DrawerItem.vue';
import Avatar from './Avatar.vue';

export default {
  name: 'Drawer',
  props: {
    user: Object
  },
  components: {
    DrawerItem,
    Avatar
  },
  data: function() {
    return {
      drawerItemDisplayText: 'inline-block',
      drawerItemIconSize: 'fa-1x',
      displayUserName: 'inline-block',
      displayCollapseButton: 'block',
      displayExpandButton: 'none',
      avatarRotateDeg: 0,
      drawerMinWidth: 70,
      drawerMaxWidth: 250,
      drawerWidth: 250
    }
  },
  methods: {
    onCollapseClick: function(e) {
      this.setTextLabelsHidde(true);
      this.displayCollapseButton = 'none',
      this.displayExpandButton = 'block';
      this.drawerItemIconSize="fa-2x";
      this.doCollapseDrawer();
      this.$refs.avatar.doRotateAvatar(-5);
    },

    onExpandClick: function() {
      this.displayCollapseButton = 'block',
      this.displayExpandButton = 'none';
      this.drawerItemIconSize="fa-1x";
      this.setTextLabelsHidde(false);
      this.doExpandDrawer();
      this.$refs.avatar.doRotateAvatar(5);
    },

    doExpandDrawer: function() {
      var me = this,
          widthStep = 5,
          collapseIntervalId = setInterval(function() {
            if(me.drawerWidth < me.drawerMaxWidth ) {
              me.drawerWidth += widthStep;
            } else {
              window.clearInterval(collapseIntervalId);
              me.drawerWidth = me.drawerMaxWidth;
              me.$emit('expand');
            }
          }, 1);
    },

    doCollapseDrawer: function() {
      var me = this,
          widthStep = 5,
          collapseIntervalId = setInterval(function() {
            if(me.drawerWidth > me.drawerMinWidth ) {
              me.drawerWidth -= widthStep;
            } else {
              window.clearInterval(collapseIntervalId);
              me.drawerWidth = me.drawerMinWidth;
              me.$emit('collapse');
            }
          }, 1);
    },

    setTextLabelsHidde: function(hidden) {
      var cssValue = (hidden? 'none': 'inline-block');
      this.drawerItemDisplayText = cssValue;
      this.displayUserName = cssValue;
    }
  }
}
</script>

<style scoped>
.wrapper {
  position: absolute;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  border: 1px solid #cdcdcd;
  margin: 5px;
  top: 0px;
  bottom: 0px;
  padding: 5px;
  box-shadow: rgba(0, 0, 0, 0.2) 0px 4px 8px 0px, rgba(0, 0, 0, 0.19) 0px 6px 20px 0px;
}

.collapseButton,
.expandButton {
  opacity: 0.5;
  margin-bottom: 10px;
}
.collapseButton {
  margin-left: auto;
  margin-right: 5px;
}

.expandButton {
  margin-left: auto;
  margin-right: auto;
}

.userName {
  border-bottom: 1px solid #cdcdcd;
  text-align: center;
  padding-bottom: 10px;
  margin-bottom: 20px;
  margin-top: 15px;
  margin-right: auto;
  margin-left: auto;
  width: 90%;
}

.menuWrapper {
  overflow:scroll;
  width: 100%;
}
.menuContainer {
  bottom: 5px;
}
</style>
