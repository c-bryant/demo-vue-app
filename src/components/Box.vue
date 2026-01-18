<script setup></script>

<template>
  <section class="box">
    <slot></slot>
  </section>
</template>

<style scoped>
.box {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  background-color: #dcdcdc;
}
</style>
