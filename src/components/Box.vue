<script setup></script>

<template>
  <div class="box">
    <slot></slot>
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
  background-color: #dcdcdc;
}
</style>
