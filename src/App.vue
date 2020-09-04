<template>
  <div class="container">
    <div class="row">
      <div class="col-sm-12 col-md-6 col-md-offset-3">
        <h2>Learning animation with Vue.js</h2>
      </div>
    </div>

    <hr>

    <!-- First exercise. Creating fade transition. -->
    <div class="row exercise-box">
      <div class="col-sm-12 col-md-6 col-md-offset-3">
        <h4>First exercise</h4>
        <button class="btn btn-success" @click="showHide1">Show/Hide</button>
        <br><br>
        <transition name="fade">
          <div class="alert alert-info" v-if="visible1">This is some info using fade transition</div>
        </transition>
      </div>
    </div>

    <hr>

    <!-- Second exercise. Creating slide animation. -->
    <div class="row exercise-box">
      <div class="col-sm-12 col-md-6 col-md-offset-3">
        <h4>Second exercise</h4>
        <button class="btn btn-success" @click="showHide2">Show/Hide</button>
        <br><br>
        <transition name="slide">
          <div class="alert alert-info" v-if="visible2">This is some info using slide animation</div>
        </transition>
      </div>
    </div>

    <!-- Third exercise. Creating fade animation and execute it on load. -->
    <div class="row exercise-box">
      <div class="col-sm-12 col-md-6 col-md-offset-3">
        <h4>Third exercise</h4>
        <p>Animate on component load</p>
        <transition name="fade" appear>
          <div class="alert alert-info">This is some info using fade animation on component load</div>
        </transition>
      </div>
    </div>


    <!-- Forth exercise. Creating animation using css framework Animate.style. -->
    <div class="row exercise-box">
      <div class="col-sm-12 col-md-6 col-md-offset-3">
        <h4>Forth exercise</h4>
        <p>Animate with Animate.style and using the attributes to specify the custom classes</p>
        <button class="btn btn-success" @click="showHide4">Show/Hide</button>
        <br><br>
        <transition enter-active-class="animate__animated animate__zoomIn"
                    leave-active-class="animate__animated animate__zoomOut"
        >
          <div class="alert alert-info" v-if="visible4">
            This is some info using fade animation using custom classes from Animate.style
          </div>
        </transition>
      </div>
    </div>


    <!-- Fifth exercise. Creating animation between two or more elements. -->
    <div class="row exercise-box">
      <div class="col-sm-12 col-md-6 col-md-offset-3">
        <h4>Fifth exercise</h4>
        <p>
          Animate between two or more elements. When more than one element is used only the v-if/v-else and so on
          can be used. v-show cannot be used.
          Remember only one element at the end can be visible at a time.
        </p>
        <p>Remember add the key attribute and the mode attribute (in-out, out-int)</p>
        <button class="btn btn-success" @click="showHide5">Switch</button>
        <br><br>
        <transition mode="out-in"
                    enter-active-class="animate__animated animate__backInUp"
                    leave-active-class="animate__animated animate__backOutDown"
        >
          <div class="alert alert-info" v-if="visible5" key="info">This is some info</div>
          <div class="alert alert-warning" v-else key="warning">This is some warning</div>
        </transition>
      </div>
    </div>

    <!-- Sixth exercise. Creating animation between two dynamic components. -->
    <div class="row exercise-box">
      <div class="col-sm-12 col-md-6 col-md-offset-3">
        <h4>Sixth exercise</h4>
        <p>
          Animate between two or more dynamic components.
          To render components dynamically use the special component called "component"
          and specify the name of the component with the attribute "is".
        </p>
        <p>Remember add the key attribute and the mode attribute (in-out, out-int)</p>
        <label for="selectComponent">Select Component</label>
        <select id="selectComponent" class="form-control"
                v-model="componentSelected">
          <option value="WarningAlert">Warning Alert</option>
          <option value="SuccessAlert">Success Alert</option>
        </select>
        <br><br>
        <transition mode="out-in"
                    enter-active-class="animate__animated animate__bounceInRight"
                    leave-active-class="animate__animated animate__bounceOutLeft"
        >
          <component :is="componentSelected"></component>
        </transition>
      </div>
    </div>

    <br><br>
  </div> <!-- container -->
</template>

<script>
import WarningAlert from "@/components/WarningAlert";
import SuccessAlert from "@/components/SuccessAlert";

export default {
  name: 'App',
  data() {
    return {
      visible1: false,
      visible2: false,
      visible4: false,
      visible5: false,
      componentSelected: 'WarningAlert'
    }
  },
  components: {
    WarningAlert,
    SuccessAlert
  },
  methods: {
    showHide1() {
      this.visible1 = !this.visible1;
    },
    showHide2() {
      this.visible2 = !this.visible2;
    },
    showHide4() {
      this.visible4 = !this.visible4;
    },
    showHide5() {
      this.visible5 = !this.visible5;
    },
  }
}
</script>

<style>
.exercise-box {
  min-height: 200px;
  border: 1px lightgray solid;
  box-shadow: 2px 2px 5px lightgray;
}

/*
* Fade transition.
* Any Vue transition with name fade will use this classes.
* But remember if the style tag is marked scoped the classes in this file will not be global.
*/
.fade-enter {
  opacity: 0;
}

.fade-enter-to {
  transition: opacity 1s;
}

.fade-leave {
  /*opacity: 1;*/
}

.fade-leave-to {
  transition: opacity 1s;
  opacity: 0;
}

/*------------------------------------------------------------------------------------------------------------------*/

/*
* Slide animation.
* Any Vue transition with name slide will use this classes.
*/
.slide-enter {
  opacity: 0;
  /*transform: translateY(20px);*/
}

.slide-enter-to {
  transition: opacity 500ms;
  animation: slide-in 1s ease-out forwards;
}

.slide-leave {
  /*opacity: 1;*/
  width: 100%;
  font-size: initial;
}

.slide-leave-to {
  opacity: 0;
  width: 0;
  font-size: 0;
  transition: opacity 500ms, width 1s, font-size 1s;
  animation: slide-out 500ms ease-out forwards;
}

@keyframes slide-in {
  from {
    transform: translateY(20px);
  }
  to {
    transform: translateY(0);
  }
}

@keyframes slide-out {
  from {
    transform: translateY(0);
  }
  to {
    transform: translateY(20px);
  }
}
</style>
