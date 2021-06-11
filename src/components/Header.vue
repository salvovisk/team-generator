<template>
  <div class="Header">
    <h2 class="Header-text">Team Generator</h2>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.Header {
  z-index: 3;
  position: relative;
  top: 0;
  width: 100vw;
  height: 10vh;
  background-color: #1d3557;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 0 10px 5px rgba(25, 25, 25, 0.4);
  display: flex;
  position: fixed;
  top: 0;
  right: 0;
  left: 0;

  &-text {
    color: #fff;
  }
}
</style>