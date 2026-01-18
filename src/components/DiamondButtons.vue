<script setup>
import { ref } from 'vue'

const props = defineProps({
  text: { type: String, default: '' },
})

const emit = defineEmits(['update:text'])

const isRainbow = ref(false)

const toggleText = () => {
  const newText = props.text === 'Sigma' ? 'Alpha' : 'Sigma'
  emit('update:text', newText)
}

const toggleRainbowColors = () => {
  isRainbow.value = !isRainbow.value
}
</script>

<template>
  <div class="btn-group">
    <button class="btn" @click="toggleText" :class="{ 'rainbow-colors': isRainbow }">A</button>
    <button class="btn" @click="toggleRainbowColors" :class="{ 'rainbow-colors': isRainbow }">
      B
    </button>
  </div>
</template>

<style scoped>
.btn-group {
  display: flex;
  flex-flow: column nowrap;
  width: 100px;
  height: 200px;
}

.btn {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 5px;
  background-color: #dc143c;
  color: #dcdcdc;
  cursor: pointer;
  font-size: 18px;
  font-weight: bold;
  width: 100%;
  height: 50%;
  clip-path: polygon(50% 0%, 100% 100%, 0% 100%);
  border: none;
  transition:
    box-shadow 0.15s ease,
    transform 0 box-shadow 0.15s ease,
    transform 0.15s ease;
  cursor: pointer;
}

.btn:active {
  box-shadow: inset 0 -4px 8px #0006;
  scale: 0.95;
}

.rainbow-colors {
  animation: rainbow 3s ease-in-out infinite alternate;
}

.btn:nth-child(2) {
  clip-path: polygon(0% 0%, 100% 0%, 50% 100%);
}

.btn:nth-child(2):active {
  box-shadow: inset 0 4px 8px #0006;
}

@keyframes rainbow {
  0% {
    filter: hue-rotate(0deg) saturate(1.5);
  }

  100% {
    filter: hue-rotate(360deg) saturate(3);
  }
}
</style>
