<template>
  <div class="container">
    <div class="row">
      <div class="col-sm-12 col-md-6 col-md-offset-3">
        <h2>Learning animation with Vue.js</h2>
      </div>
    </div>

    <hr>

    <!-- First exercise. Creating fade transition. -->
    <div class="row">
      <div class="col-sm-12 col-md-6 col-md-offset-3">
        <h4>First exercise</h4>
        <button class="btn btn-success" @click="showHide">Show/Hide</button>
        <br><br>
        <transition name="fade">
          <div class="alert alert-info" v-if="visible">This is some info</div>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      visible: false
    }
  },
  components: {},
  methods: {
    showHide() {
      this.visible = !this.visible;
    }
  }
}
</script>

<style>
/*
* Fade transition.
* Any Vue transition with name fade will use this classes.
* But remember if the style tag is marked scoped the classes in this file will not be global.
*/
.fade-enter {
  opacity: 0;
}

.fade-enter-active {
  transition: opacity 1s;
}

.fade-leave {
  /*opacity: 1;*/
}

.fade-leave-active {
  transition: opacity 1s;
  opacity: 0;
}
</style>
