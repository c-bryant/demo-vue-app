<script setup>
import Box from './components/Box.vue'
import DiamondButtons from './components/DiamondButtons.vue'
import { ref, onMounted, onBeforeUnmount } from 'vue'

const text = ref('Sigma')

const isRainbow = ref(false)

const fontLoaded = ref(false)

const onToggleClick = () => {
  text.value = text.value === 'Sigma' ? 'Alpha' : 'Sigma'
}

const isSpinning = ref(true)
let spinPauseTimer = null

const onSpinEnd = () => {
  isSpinning.value = false
  spinPauseTimer = setTimeout(() => {
    isSpinning.value = true
  }, 8000)
}

onMounted(async () => {
  isSpinning.value = false
  spinPauseTimer = setTimeout(() => {
    isSpinning.value = true
  }, 8000)

  // Load the Exile font and avoid showing the stylized text until it's ready.
  // Use a short timeout fallback so the UI doesn't stay hidden forever.
  try {
    if (typeof document !== 'undefined' && document.fonts && document.fonts.load) {
      const loadPromise = document.fonts.load('1em "Exile"')
      const timeout = new Promise((res) => setTimeout(res, 3000))
      await Promise.race([loadPromise, timeout])
    }
  } catch (err) {
    // ignore font loading errors
  }

  fontLoaded.value = true
})

onBeforeUnmount(() => {
  if (spinPauseTimer) clearTimeout(spinPauseTimer)
})
</script>

<template>
  <div class="boxes-container">
    <!-- Top-left quadrant -->
    <Box class="quadrant tl">
      <span v-if="fontLoaded" class="stylized-text exile-regular">{{ text }}</span>
    </Box>

    <!-- Top-right quadrant -->
    <Box class="quadrant tr" style="border-radius: 0 100% 0 0" />

    <!-- Bottom-left quadrant -->
    <Box class="quadrant bl">
      <img
        :class="['crest-image', { spinning: isSpinning }]"
        src="../public/assets/mcgregor_crest_coat_of_arms.png"
        alt="mcgreggor crest coat of arms"
        @animationend="onSpinEnd"
      />
    </Box>

    <!-- Bottom-right quadrant -->
    <Box class="quadrant br">
      <div class="box-content">
        <DiamondButtons
          :isRainbow="isRainbow"
          @textToggle="onToggleClick"
          @rainbowToggle="isRainbow = !isRainbow"
        />
      </div>
    </Box>
  </div>
</template>

<style>
.exile-regular {
  font-family: 'Exile', system-ui;
  font-weight: 400;
  font-style: normal;
}

.boxes-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 10px;
  height: calc(100vh - 20px);
  margin: 0 auto;
  place-items: center;
}

.quadrant {
  width: 100%;
  height: 100%;
  box-sizing: border-box;
}

.stylized-text {
  font-weight: 400;
  color: rgb(31, 29, 29);
  font-family: Exile, system-ui;
  font-size: 64px;
}

@keyframes spin-once {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

/* When .spinning is present, run exactly one rotation so animationend fires */
.crest-image.spinning {
  animation: spin-once 8s linear 1;
}
</style>
