<template lang="html">
  <div v-if="loading">
    <div class="pre-loader d-flex justify-content-center">
      <div class="loading">
        <div class="beer-like cheer">
          <svg class="right">
            <use href="#beer"></use>
          </svg>
          <svg class="left">
            <use href="#beer"></use>
          </svg>
        </div>
      </div>
    </div>
    <icons></icons>
  </div>
</template>

<script>
export default {
  data: () => ({
    loading: false,
  }),
  methods: {
    start() {
      this.loading = true
    },
    finish() {
      this.loading = false
    },
  },
}
</script>

<style>
.pre-loader {
  z-index: 9999;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  align-items: center;
  background: black;
}
.loading {
  width: 600px;
  overflow: auto;
  overflow: hidden;
}
.beer-like {
  width: 100px;
  height: 100px;
  --primary: #c45e1a;
  --secondary: #771a14;
  position: relative;
  outline: none;
  border: none;
  padding: 0;
  margin: 0 auto;
  -webkit-appearance: none;
  -webkit-tap-highlight-color: transparent;
}
.beer-like svg {
  width: 60px;
  height: 68px;
  display: block;
  fill: #fff;
  z-index: 1;
  stroke: var(--stroke, var(--primary));
  position: absolute;
  left: 35px;
  top: 31px;
  transform: scaleX(var(--scale-x, 1)) rotate(10deg)
    translate(var(--x, -15px), var(--y, 4px)) translateZ(0);
}
.beer-like svg.right {
  --stroke: var(--secondary);
  --scale-x: -1;
  --y: -4px;
}
.beer-like.cheer svg {
  animation: cheer 1.1s infinite;
}
@keyframes cheer {
  35% {
    transform: scaleX(var(--scale-x, 1)) rotate(20deg)
      translate(-36px, var(--y, 8px)) translateZ(0);
  }
  55% {
    transform: scaleX(var(--scale-x, 1)) rotate(16deg)
      translate(-9px, var(--y, 8px)) translateZ(0);
  }
}
</style>
