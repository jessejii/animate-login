<template>
  <div class="relative flex items-end justify-center h-[500px]">
    <!-- Cartoon Characters -->
    <div class="relative" style="width: 550px; height: 400px;">
      <!-- Purple tall rectangle character - Back layer -->
      <div class="absolute bottom-0 character-drop character-drop--purple" :class="{ 'character-drop--ready': isEntranceReady }">
        <div
          ref="purpleRef"
          class="absolute bottom-0 transition-all duration-700 ease-in-out"
          :class="{ 'error-wiggle-purple': isErrorExpressionActive }"
          :style="{
            left: '70px',
          width: '180px',
          height: (isTyping || (password.length > 0 && !showPassword)) ? '440px' : '400px',
          backgroundColor: '#6C3FF5',
          borderRadius: '10px 10px 0 0',
          zIndex: 1,
          transform: (password.length > 0 && showPassword)
            ? 'skewX(0deg)'
            : (isTyping || (password.length > 0 && !showPassword))
              ? `skewX(${purplePos.bodySkew - 12}deg) translateX(40px)`
              : `skewX(${purplePos.bodySkew}deg)`,
          transformOrigin: 'bottom center',
        }"
      >
        <!-- Eyes -->
        <div
          class="absolute flex gap-8 transition-all duration-700 ease-in-out"
          :style="{
            left: (password.length > 0 && showPassword) ? '20px' : isLookingAtEachOther ? '55px' : `${45 + purplePos.faceX}px`,
            top: (password.length > 0 && showPassword) ? '35px' : isLookingAtEachOther ? '65px' : `${40 + purplePos.faceY}px`,
          }"
        >
          <EyeBall
            :size="18"
            :pupil-size="7"
            :max-distance="5"
            eye-color="white"
            pupil-color="#2D2D2D"
            :is-blinking="isPurpleBlinking"
            :force-look-x="(password.length > 0 && showPassword) ? (isPurplePeeking ? 4 : -4) : isErrorExpressionActive ? 0 : isLookingAtEachOther ? 3 : undefined"
            :force-look-y="(password.length > 0 && showPassword) ? (isPurplePeeking ? 5 : -4) : isErrorExpressionActive ? 5 : isLookingAtEachOther ? 4 : undefined"
          />
          <EyeBall
            :size="18"
            :pupil-size="7"
            :max-distance="5"
            eye-color="white"
            pupil-color="#2D2D2D"
            :is-blinking="isPurpleBlinking"
            :force-look-x="(password.length > 0 && showPassword) ? (isPurplePeeking ? 4 : -4) : isErrorExpressionActive ? 0 : isLookingAtEachOther ? 3 : undefined"
            :force-look-y="(password.length > 0 && showPassword) ? (isPurplePeeking ? 5 : -4) : isErrorExpressionActive ? 5 : isLookingAtEachOther ? 4 : undefined"
          />
        </div>

        <div
          v-if="isErrorExpressionActive"
          class="absolute rounded-full"
          :style="{
            left: `${118 + purplePos.faceX}px`,
            top: `${72 + purplePos.faceY}px`,
            width: '9px',
            height: '14px',
            backgroundColor: 'rgba(178, 226, 255, 0.95)',
            transform: 'rotate(12deg)',
          }"
        />
      </div>
      </div>

      <!-- Black tall rectangle character - Middle layer -->
      <div class="absolute bottom-0 character-drop character-drop--black" :class="{ 'character-drop--ready': isEntranceReady }">
        <div
          ref="blackRef"
          class="absolute bottom-0 transition-all duration-700 ease-in-out"
          :class="{ 'error-shake-black': isErrorExpressionActive }"
          :style="{
            left: '240px',
          width: '120px',
          height: '310px',
          backgroundColor: '#2D2D2D',
          borderRadius: '8px 8px 0 0',
          zIndex: 2,
          transform: (password.length > 0 && showPassword)
            ? 'skewX(0deg)'
            : isLookingAtEachOther
              ? `skewX(${blackPos.bodySkew * 1.5 + 10}deg) translateX(20px)`
              : (isTyping || (password.length > 0 && !showPassword))
                ? `skewX(${blackPos.bodySkew * 1.5}deg)`
                : `skewX(${blackPos.bodySkew}deg)`,
          transformOrigin: 'bottom center',
        }"
      >
        <!-- Eyes -->
        <div
          class="absolute flex gap-6 transition-all duration-700 ease-in-out"
          :style="{
            left: (password.length > 0 && showPassword) ? '10px' : isLookingAtEachOther ? '32px' : `${26 + blackPos.faceX}px`,
            top: (password.length > 0 && showPassword) ? '28px' : isLookingAtEachOther ? '12px' : `${32 + blackPos.faceY}px`,
          }"
        >
          <EyeBall
            :size="16"
            :pupil-size="6"
            :max-distance="4"
            eye-color="white"
            pupil-color="#2D2D2D"
            :is-blinking="isBlackBlinking"
            :force-look-x="(password.length > 0 && showPassword) ? -4 : isErrorExpressionActive ? -1 : isLookingAtEachOther ? 0 : undefined"
            :force-look-y="(password.length > 0 && showPassword) ? -4 : isErrorExpressionActive ? 5 : isLookingAtEachOther ? -4 : undefined"
          />
          <EyeBall
            :size="16"
            :pupil-size="6"
            :max-distance="4"
            eye-color="white"
            pupil-color="#2D2D2D"
            :is-blinking="isBlackBlinking"
            :force-look-x="(password.length > 0 && showPassword) ? -4 : isErrorExpressionActive ? -1 : isLookingAtEachOther ? 0 : undefined"
            :force-look-y="(password.length > 0 && showPassword) ? -4 : isErrorExpressionActive ? 5 : isLookingAtEachOther ? -4 : undefined"
          />
        </div>

        <div
          class="absolute transition-all duration-200 ease-out"
          :style="{
            left: `${44 + blackPos.faceX}px`,
            top: `${90 + blackPos.faceY}px`,
            width: isErrorExpressionActive ? '30px' : '24px',
            height: isErrorExpressionActive ? '10px' : '4px',
            backgroundColor: '#f7f7f7',
            borderRadius: isErrorExpressionActive ? '12px 12px 0 0' : '6px',
          }"
        />

        <div
          v-if="isErrorExpressionActive"
          class="absolute rounded-full"
          :style="{
            left: `${86 + blackPos.faceX}px`,
            top: `${68 + blackPos.faceY}px`,
            width: '7px',
            height: '11px',
            backgroundColor: 'rgba(178, 226, 255, 0.95)',
            transform: 'rotate(18deg)',
          }"
        />
      </div>
      </div>

      <!-- Orange semi-circle character - Front left (Cute version with expressions) -->
      <div class="absolute bottom-0 character-drop character-drop--orange" :class="{ 'character-drop--ready': isEntranceReady }">
        <div
          ref="orangeRef"
          class="absolute bottom-0 transition-all duration-700 ease-in-out"
          :class="{ 'error-bounce': isErrorExpressionActive }"
          :style="{
            left: '0px',
          width: '240px',
          height: '200px',
          zIndex: 3,
          backgroundColor: '#FF9B6B',
          borderRadius: '120px 120px 0 0',
          transform: (password.length > 0 && showPassword) ? 'skewX(0deg)' : `skewX(${orangePos.bodySkew}deg)`,
          transformOrigin: 'bottom center',
        }"
      >
        <!-- Blush (腮红) -->
        <div
          class="absolute transition-all duration-300 ease-out"
          :style="{
            left: `${25 + orangePos.faceX * 0.5}px`,
            top: `${105 + orangePos.faceY * 0.3}px`,
            width: '25px',
            height: '12px',
            backgroundColor: 'rgba(255, 120, 120, 0.5)',
            borderRadius: '50%',
            transform: `scale(${orangeExpression.blushScale})`,
          }"
        />
        <div
          class="absolute transition-all duration-300 ease-out"
          :style="{
            right: `${45 - orangePos.faceX * 0.5}px`,
            top: `${105 + orangePos.faceY * 0.3}px`,
            width: '25px',
            height: '12px',
            backgroundColor: 'rgba(255, 120, 120, 0.5)',
            borderRadius: '50%',
            transform: `scale(${orangeExpression.blushScale})`,
          }"
        />

        <!-- Cute tears on login error -->
        <div
          v-if="isErrorExpressionActive"
          class="absolute rounded-full transition-all duration-200"
          :style="{
            left: `${84 + orangePos.faceX}px`,
            top: `${102 + orangePos.faceY}px`,
            width: '8px',
            height: '12px',
            backgroundColor: 'rgba(180, 224, 255, 0.95)',
            transform: 'rotate(-8deg)',
          }"
        />
        <div
          v-if="isErrorExpressionActive"
          class="absolute rounded-full transition-all duration-200"
          :style="{
            left: `${126 + orangePos.faceX}px`,
            top: `${102 + orangePos.faceY}px`,
            width: '8px',
            height: '12px',
            backgroundColor: 'rgba(180, 224, 255, 0.95)',
            transform: 'rotate(8deg)',
          }"
        />

        <!-- Eyebrows (眉毛) -->
        <div
          class="absolute transition-all duration-300 ease-out"
          :style="{
            left: (password.length > 0 && showPassword) ? '48px' : `${72 + orangePos.faceX}px`,
            top: (password.length > 0 && showPassword) ? '72px' : `${68 + orangePos.faceY}px`,
            width: '22px',
            height: '4px',
            backgroundColor: '#2D2D2D',
            borderRadius: '2px',
            transform: `rotate(${orangeExpression.leftEyebrowRotate}deg)`,
          }"
        />
        <div
          class="absolute transition-all duration-300 ease-out"
          :style="{
            left: (password.length > 0 && showPassword) ? '82px' : `${156 + orangePos.faceX}px`,
            top: (password.length > 0 && showPassword) ? '72px' : `${68 + orangePos.faceY}px`,
            width: '22px',
            height: '4px',
            backgroundColor: '#2D2D2D',
            borderRadius: '2px',
            transform: `rotate(${orangeExpression.rightEyebrowRotate}deg)`,
          }"
        />

        <!-- Eyes with blinking -->
        <div
          class="absolute flex gap-8 transition-all duration-200 ease-out"
          :style="{
            left: (password.length > 0 && showPassword) ? '50px' : `${75 + orangePos.faceX}px`,
            top: (password.length > 0 && showPassword) ? '85px' : `${82 + orangePos.faceY}px`,
          }"
        >
          <!-- Left Eye -->
          <div
            class="relative transition-all duration-150"
            :style="{
              width: '20px',
              height: isOrangeBlinking ? '2px' : orangeExpression.eyeHeight + 'px',
              borderRadius: isOrangeBlinking ? '2px' : '50%',
              backgroundColor: '#2D2D2D',
              overflow: 'hidden',
            }"
          >
            <!-- Eye shine -->
            <div
              v-if="!isOrangeBlinking"
              class="absolute bg-white rounded-full transition-all duration-200"
              :style="{
                width: '6px',
                height: '6px',
                left: orangeExpression.eyeShineX + 'px',
                top: '3px',
              }"
            />
          </div>
          <!-- Right Eye -->
          <div
            class="relative transition-all duration-150"
            :style="{
              width: '20px',
              height: isOrangeBlinking ? '2px' : orangeExpression.eyeHeight + 'px',
              borderRadius: isOrangeBlinking ? '2px' : '50%',
              backgroundColor: '#2D2D2D',
              overflow: 'hidden',
            }"
          >
            <!-- Eye shine -->
            <div
              v-if="!isOrangeBlinking"
              class="absolute bg-white rounded-full transition-all duration-200"
              :style="{
                width: '6px',
                height: '6px',
                left: orangeExpression.eyeShineX + 'px',
                top: '3px',
              }"
            />
          </div>
        </div>

        <!-- Mouth with expressions -->
        <div
          class="absolute transition-all duration-300 ease-out"
          :style="{
            left: (password.length > 0 && showPassword) ? '70px' : `${100 + orangePos.faceX}px`,
            top: (password.length > 0 && showPassword) ? '115px' : `${118 + orangePos.faceY}px`,
            width: orangeExpression.mouthWidth + 'px',
            height: orangeExpression.mouthHeight + 'px',
            backgroundColor: '#2D2D2D',
            borderRadius: orangeExpression.mouthRadius,
            transform: `rotate(${orangeExpression.mouthRotate}deg)`,
          }"
        />
      </div>
      </div>

      <!-- Yellow tall rectangle character - Front right -->
      <div class="absolute bottom-0 character-drop character-drop--yellow" :class="{ 'character-drop--ready': isEntranceReady }">
        <div
          ref="yellowRef"
          class="absolute bottom-0 transition-all duration-700 ease-in-out"
          :class="{ 'error-pop-yellow': isErrorExpressionActive }"
          :style="{
            left: '310px',
          width: '140px',
          height: '230px',
          backgroundColor: '#E8D754',
          borderRadius: '70px 70px 0 0',
          zIndex: 4,
          transform: (password.length > 0 && showPassword) ? 'skewX(0deg)' : `skewX(${yellowPos.bodySkew}deg)`,
          transformOrigin: 'bottom center',
        }"
      >
        <!-- Eyes - just pupils, no white -->
        <div
          class="absolute flex gap-6 transition-all duration-200 ease-out"
          :style="{
            left: (password.length > 0 && showPassword) ? '20px' : `${52 + yellowPos.faceX}px`,
            top: (password.length > 0 && showPassword) ? '35px' : `${40 + yellowPos.faceY}px`,
          }"
        >
          <Pupil
            :size="12"
            :max-distance="5"
            pupil-color="#2D2D2D"
            :force-look-x="(password.length > 0 && showPassword) ? -5 : isErrorExpressionActive ? 0 : undefined"
            :force-look-y="(password.length > 0 && showPassword) ? -4 : isErrorExpressionActive ? 5 : undefined"
          />
          <Pupil
            :size="12"
            :max-distance="5"
            pupil-color="#2D2D2D"
            :force-look-x="(password.length > 0 && showPassword) ? -5 : isErrorExpressionActive ? 0 : undefined"
            :force-look-y="(password.length > 0 && showPassword) ? -4 : isErrorExpressionActive ? 5 : undefined"
          />
        </div>

        <div
          v-if="isErrorExpressionActive"
          class="absolute rounded-full"
          :style="{
            left: `${102 + yellowPos.faceX}px`,
            top: `${58 + yellowPos.faceY}px`,
            width: '7px',
            height: '11px',
            backgroundColor: 'rgba(178, 226, 255, 0.95)',
            transform: 'rotate(14deg)',
          }"
        />

        <!-- Horizontal line for mouth -->
        <div
          class="absolute transition-all duration-200 ease-out"
          :style="{
            left: (password.length > 0 && showPassword) ? '10px' : `${40 + yellowPos.faceX}px`,
            top: (password.length > 0 && showPassword) ? '88px' : `${88 + yellowPos.faceY}px`,
            width: isErrorExpressionActive ? '42px' : '80px',
            height: isErrorExpressionActive ? '12px' : '4px',
            backgroundColor: '#2D2D2D',
            borderRadius: isErrorExpressionActive ? '10px 10px 0 0' : '999px',
          }"
        />
      </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted, computed, watch } from 'vue'
import EyeBall from './EyeBall.vue'
import Pupil from './Pupil.vue'

const props = defineProps<{
  isTyping: boolean
  password: string
  showPassword: boolean
  loginErrorTick: number
}>()

const mouseX = ref(0)
const mouseY = ref(0)
const isPurpleBlinking = ref(false)
const isBlackBlinking = ref(false)
const isOrangeBlinking = ref(false)
const isLookingAtEachOther = ref(false)
const isPurplePeeking = ref(false)
const isEntranceReady = ref(false)
const isErrorExpressionActive = ref(false)

const purpleRef = ref<HTMLElement | null>(null)
const blackRef = ref<HTMLElement | null>(null)
const yellowRef = ref<HTMLElement | null>(null)
const orangeRef = ref<HTMLElement | null>(null)

const calculatePosition = (ref: HTMLElement | null) => {
  if (!ref) return { faceX: 0, faceY: 0, bodySkew: 0 }

  const rect = ref.getBoundingClientRect()
  const centerX = rect.left + rect.width / 2
  const centerY = rect.top + rect.height / 3

  const deltaX = mouseX.value - centerX
  const deltaY = mouseY.value - centerY

  const faceX = Math.max(-15, Math.min(15, deltaX / 20))
  const faceY = Math.max(-10, Math.min(10, deltaY / 30))
  const bodySkew = Math.max(-6, Math.min(6, -deltaX / 120))

  return { faceX, faceY, bodySkew }
}

const purplePos = computed(() => calculatePosition(purpleRef.value))
const blackPos = computed(() => calculatePosition(blackRef.value))
const yellowPos = computed(() => calculatePosition(yellowRef.value))
const orangePos = computed(() => calculatePosition(orangeRef.value))

const orangeExpression = computed(() => {
  const skew = orangePos.value.bodySkew
  const isPeeking = props.password.length > 0 && props.showPassword
  const isError = isErrorExpressionActive.value

  let expression = {
    eyeHeight: 18,
    eyeShineX: 4,
    mouthWidth: 30,
    mouthHeight: 14,
    mouthRadius: '0 0 15px 15px',
    mouthRotate: 0,
    leftEyebrowRotate: 0,
    rightEyebrowRotate: 0,
    blushScale: 1,
  }

  if (isError) {
    expression = {
      ...expression,
      eyeHeight: 12,
      eyeShineX: 1,
      mouthWidth: 18,
      mouthHeight: 8,
      mouthRadius: '10px 10px 0 0',
      mouthRotate: 0,
      leftEyebrowRotate: -25,
      rightEyebrowRotate: 25,
      blushScale: 1.5,
    }
  } else if (isPeeking) {
    expression = {
      ...expression,
      eyeHeight: 10,
      eyeShineX: 2,
      mouthWidth: 20,
      mouthHeight: 6,
      mouthRadius: '3px',
      mouthRotate: -10,
      leftEyebrowRotate: -15,
      rightEyebrowRotate: 15,
      blushScale: 1.3,
    }
  } else if (skew < -3) {
    expression = {
      ...expression,
      eyeHeight: 22,
      eyeShineX: 5,
      mouthWidth: 20,
      mouthHeight: 20,
      mouthRadius: '50%',
      mouthRotate: 0,
      leftEyebrowRotate: -20,
      rightEyebrowRotate: -20,
      blushScale: 1.2,
    }
  } else if (skew > 3) {
    expression = {
      ...expression,
      eyeHeight: 16,
      eyeShineX: 3,
      mouthWidth: 35,
      mouthHeight: 10,
      mouthRadius: '0 0 20px 20px',
      mouthRotate: 8,
      leftEyebrowRotate: 10,
      rightEyebrowRotate: -5,
      blushScale: 1.4,
    }
  } else {
    expression = {
      ...expression,
      eyeHeight: 18,
      eyeShineX: 4,
      mouthWidth: 32,
      mouthHeight: 16,
      mouthRadius: '0 0 16px 16px',
      mouthRotate: 0,
      leftEyebrowRotate: 0,
      rightEyebrowRotate: 0,
      blushScale: 1,
    }
  }

  return expression
})

const handleMouseMove = (e: MouseEvent) => {
  mouseX.value = e.clientX
  mouseY.value = e.clientY
}

const getRandomBlinkInterval = () => Math.random() * 4000 + 3000

let isUnmounted = false
let purpleBlinkTimeout: ReturnType<typeof setTimeout> | null = null
let blackBlinkTimeout: ReturnType<typeof setTimeout> | null = null
let orangeBlinkTimeout: ReturnType<typeof setTimeout> | null = null
let entranceTimer: ReturnType<typeof setTimeout> | null = null
let typingLookTimer: ReturnType<typeof setTimeout> | null = null
let purplePeekTimeout: ReturnType<typeof setTimeout> | null = null
let purplePeekEndTimeout: ReturnType<typeof setTimeout> | null = null
let errorExpressionTimer: ReturnType<typeof setTimeout> | null = null

const clearTimer = (timer: ReturnType<typeof setTimeout> | null) => {
  if (timer) clearTimeout(timer)
}

const scheduleBlink = (
  setBlinking: (value: boolean) => void,
  assignTimer: (timer: ReturnType<typeof setTimeout>) => void,
) => {
  assignTimer(
    setTimeout(() => {
      if (isUnmounted) return

      setBlinking(true)

      assignTimer(
        setTimeout(() => {
          if (isUnmounted) return

          setBlinking(false)
          scheduleBlink(setBlinking, assignTimer)
        }, 150),
      )
    }, getRandomBlinkInterval()),
  )
}

const stopPurplePeekLoop = () => {
  clearTimer(purplePeekTimeout)
  clearTimer(purplePeekEndTimeout)
  purplePeekTimeout = null
  purplePeekEndTimeout = null
  isPurplePeeking.value = false
}

const startPurplePeekLoop = () => {
  stopPurplePeekLoop()

  purplePeekTimeout = setTimeout(() => {
    if (isUnmounted) return

    isPurplePeeking.value = true

    purplePeekEndTimeout = setTimeout(() => {
      if (isUnmounted) return

      isPurplePeeking.value = false
      startPurplePeekLoop()
    }, 800)
  }, Math.random() * 3000 + 2000)
}

onMounted(() => {
  isUnmounted = false
  window.addEventListener('mousemove', handleMouseMove)

  entranceTimer = setTimeout(() => {
    isEntranceReady.value = true
  }, 120)

  scheduleBlink(
    (value) => {
      isPurpleBlinking.value = value
    },
    (timer) => {
      purpleBlinkTimeout = timer
    },
  )

  scheduleBlink(
    (value) => {
      isBlackBlinking.value = value
    },
    (timer) => {
      blackBlinkTimeout = timer
    },
  )

  scheduleBlink(
    (value) => {
      isOrangeBlinking.value = value
    },
    (timer) => {
      orangeBlinkTimeout = timer
    },
  )
})

onUnmounted(() => {
  isUnmounted = true
  window.removeEventListener('mousemove', handleMouseMove)

  clearTimer(purpleBlinkTimeout)
  clearTimer(blackBlinkTimeout)
  clearTimer(orangeBlinkTimeout)
  clearTimer(entranceTimer)
  clearTimer(typingLookTimer)
  clearTimer(errorExpressionTimer)
  stopPurplePeekLoop()
})

watch(
  () => props.isTyping,
  (newValue) => {
    clearTimer(typingLookTimer)
    typingLookTimer = null

    if (newValue) {
      isLookingAtEachOther.value = true
      typingLookTimer = setTimeout(() => {
        if (isUnmounted) return
        isLookingAtEachOther.value = false
      }, 800)
      return
    }

    isLookingAtEachOther.value = false
  },
)

watch(
  () => props.loginErrorTick,
  (newTick, oldTick) => {
    if (!newTick || newTick === oldTick) return

    clearTimer(errorExpressionTimer)
    isErrorExpressionActive.value = false

    requestAnimationFrame(() => {
      if (isUnmounted) return
      isErrorExpressionActive.value = true
    })

    errorExpressionTimer = setTimeout(() => {
      if (isUnmounted) return
      isErrorExpressionActive.value = false
    }, 1800)
  },
)

watch(
  [() => props.password, () => props.showPassword],
  ([newPassword, newShowPassword]) => {
    if (newPassword.length > 0 && newShowPassword) {
      startPurplePeekLoop()
      return
    }

    stopPurplePeekLoop()
  },
)
</script>

<style scoped>
.character-drop {
  opacity: 0;
  transform: translateY(-320px) scale(0.92);
  transform-origin: bottom center;
  will-change: transform, opacity;
}

.character-drop--ready {
  opacity: 1;
}

.character-drop--purple.character-drop--ready {
  animation: dropPurple 1s cubic-bezier(0.22, 1.1, 0.3, 1) forwards;
}

.character-drop--black.character-drop--ready {
  animation: dropBlack 0.95s cubic-bezier(0.2, 1, 0.32, 1) 0.08s forwards;
}

.character-drop--orange.character-drop--ready {
  animation: dropOrange 1.08s cubic-bezier(0.18, 1.15, 0.3, 1) 0.04s forwards;
}

.character-drop--yellow.character-drop--ready {
  animation: dropYellow 1.02s cubic-bezier(0.22, 1.08, 0.3, 1) 0.12s forwards;
}

.error-bounce {
  animation: errorBounce 0.62s ease-out;
}

.error-wiggle-purple {
  animation: errorWigglePurple 0.64s ease-out;
}

.error-shake-black {
  animation: errorShakeBlack 0.56s ease-out;
}

.error-pop-yellow {
  animation: errorPopYellow 0.58s ease-out;
}

@keyframes dropPurple {
  0% { transform: translateY(-340px) scale(0.9) rotate(-8deg); }
  60% { transform: translateY(22px) scale(1.02) rotate(3deg); }
  78% { transform: translateY(-10px) scale(0.99) rotate(-2deg); }
  100% { transform: translateY(0) scale(1) rotate(0deg); }
}

@keyframes dropBlack {
  0% { transform: translateY(-300px) scale(0.94) rotate(7deg); }
  62% { transform: translateY(16px) scale(1.01) rotate(-4deg); }
  82% { transform: translateY(-7px) scale(1) rotate(2deg); }
  100% { transform: translateY(0) scale(1) rotate(0deg); }
}

@keyframes dropOrange {
  0% { transform: translateY(-360px) scale(0.88) rotate(-10deg); }
  58% { transform: translateY(30px) scale(1.04) rotate(6deg); }
  74% { transform: translateY(-14px) scale(0.98) rotate(-3deg); }
  88% { transform: translateY(6px) scale(1.01) rotate(2deg); }
  100% { transform: translateY(0) scale(1) rotate(0deg); }
}

@keyframes dropYellow {
  0% { transform: translateY(-320px) scale(0.9) rotate(9deg); }
  60% { transform: translateY(20px) scale(1.03) rotate(-5deg); }
  80% { transform: translateY(-9px) scale(0.99) rotate(2deg); }
  100% { transform: translateY(0) scale(1) rotate(0deg); }
}

@keyframes errorBounce {
  0% { transform: translateY(0) rotate(0deg); }
  20% { transform: translateY(-8px) rotate(-4deg); }
  42% { transform: translateY(5px) rotate(3deg); }
  65% { transform: translateY(-3px) rotate(-2deg); }
  100% { transform: translateY(0) rotate(0deg); }
}

@keyframes errorWigglePurple {
  0% { transform: translateY(0) rotate(0deg); }
  25% { transform: translateY(-6px) rotate(-5deg); }
  55% { transform: translateY(3px) rotate(4deg); }
  80% { transform: translateY(-2px) rotate(-2deg); }
  100% { transform: translateY(0) rotate(0deg); }
}

@keyframes errorShakeBlack {
  0% { transform: translateX(0); }
  20% { transform: translateX(-6px); }
  40% { transform: translateX(5px); }
  60% { transform: translateX(-4px); }
  80% { transform: translateX(2px); }
  100% { transform: translateX(0); }
}

@keyframes errorPopYellow {
  0% { transform: translateY(0) scale(1); }
  30% { transform: translateY(-10px) scale(1.04); }
  60% { transform: translateY(4px) scale(0.98); }
  100% { transform: translateY(0) scale(1); }
}
</style>
