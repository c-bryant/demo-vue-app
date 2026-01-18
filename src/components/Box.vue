<script setup></script>

<template>
  <div class="box">
    <div class="box-content">
      <slot></slot>
    </div>
  </div>
</template>

<style scoped>
.box {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0;
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  padding: 8px;
  background-color: lightgray;
}

.box-content {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Make slotted .box-content fill and scale inside the box. */
::v-deep .box-content {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

::v-deep .box-content > * {
  max-width: 100%;
  max-height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Images scale to fit the box while preserving aspect ratio */
::v-deep .box-content img {
  width: auto;
  height: 100%;
  max-height: 320px;
  max-width: 100%;
  object-fit: contain;
}

/* Responsive text sizing for slotted text; parent rules still apply but this ensures scaling */
::v-deep .box-content .stylized-text,
::v-deep .box-content .stylized-text {
  font-size: 4em;
  line-height: 1;
  text-align: center;
}

/* Ensure buttons don't overflow on small boxes */
::v-deep .box-content .btn {
  transform-origin: center;
  max-width: 90%;
  box-sizing: border-box;
}
</style>
