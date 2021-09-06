<template>
  <div>
    <div class="icon-wrapper" v-html="svg"></div>
    <slot></slot>
  </div>
</template>

<style scoped>
.icon-wrapper {
  display: inline-flex;
  align-items: center;
  color: rgba(0, 0, 0, 0.4);
  font-size: 1rem;
  font-weight: 600;
  margin-right: 6px;
}
.icon {
  stroke: currentColor;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
  fill: none;
}
</style>

<script>
import feather from 'feather-icons'
export default {
  props: {
    name: String, // the name of the symbol we want to use
    width: {
      type: [Number, String],
      default: 24
    },
    height: {
      type: [Number, String],
      default: 24
    }
  },
  computed: {
    svg() {
      /**
       * we get an icon from the icons dictionary by name, for example, "activity" for the "activity icon". And then,
       * we use the "toSvg" method to get the SVG of the icon. The class property is a configuration option that we use
       * to add a class attribute to the SVG.
      */
      return feather.icons[this.name].toSvg({ 
        class: "icon",
        width: this.width,
        height: this.height
      })
    }
  }
}
</script>
