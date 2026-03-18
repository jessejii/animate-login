<template>
  <div class="min-h-screen grid lg:grid-cols-2">
    <!-- Left Content Section -->
    <div class="relative hidden lg:flex flex-col justify-between bg-gradient-to-br from-primary/90 via-primary to-primary/80 p-12 text-primary-foreground">
      <div class="relative z-20">
        <div class="flex items-center gap-2 text-lg font-semibold">
          <div class="size-8 rounded-lg bg-primary-foreground/10 backdrop-blur-sm flex items-center justify-center">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="m12 3-1.912 5.813a2 2 0 0 1-1.275 1.275L3 12l5.813 1.912a2 2 0 0 1 1.275 1.275L12 21l1.912-5.813a2 2 0 0 1 1.275-1.275L21 12l-5.813-1.912a2 2 0 0 1-1.275-1.275L12 3Z"/>
            </svg>
          </div>
          <span>YourBrand</span>
        </div>
      </div>

      <!-- Animated Characters Component -->
      <AnimatedCharacters
        :is-typing="isTyping"
        :password="password"
        :show-password="showPassword"
        :login-error-tick="loginErrorTick"
      />

      <div class="relative z-20 flex items-center gap-8 text-sm text-primary-foreground/60">
        <a href="#" class="hover:text-primary-foreground transition-colors">
          Privacy Policy
        </a>
        <a href="#" class="hover:text-primary-foreground transition-colors">
          Terms of Service
        </a>
        <a href="#" class="hover:text-primary-foreground transition-colors">
          Contact
        </a>
      </div>

      <!-- Decorative elements -->
      <div class="absolute inset-0 bg-grid-white/[0.05] bg-[size:20px_20px]" />
      <div class="absolute top-1/4 right-1/4 size-64 bg-primary-foreground/10 rounded-full blur-3xl" />
      <div class="absolute bottom-1/4 left-1/4 size-96 bg-primary-foreground/5 rounded-full blur-3xl" />
    </div>

    <!-- Right Login Section -->
    <div class="flex items-center justify-center p-8 bg-background">
      <div class="w-full max-w-[420px]">
        <!-- Mobile Logo -->
        <div class="lg:hidden flex items-center justify-center gap-2 text-lg font-semibold mb-12">
          <div class="size-8 rounded-lg bg-primary/10 flex items-center justify-center">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="m12 3-1.912 5.813a2 2 0 0 1-1.275 1.275L3 12l5.813 1.912a2 2 0 0 1 1.275 1.275L12 21l1.912-5.813a2 2 0 0 1 1.275-1.275L21 12l-5.813-1.912a2 2 0 0 1-1.275-1.275L12 3Z"/>
            </svg>
          </div>
          <span>YourBrand</span>
        </div>

        <!-- Header -->
        <div class="text-center mb-10">
          <h1 class="text-3xl font-bold tracking-tight mb-2">Welcome back!</h1>
          <p class="text-muted-foreground text-sm">Please enter your details</p>
        </div>

        <!-- Login Form -->
        <form @submit.prevent="handleSubmit" class="space-y-5">
          <div class="space-y-2">
            <label for="email" class="text-sm font-medium leading-none">Email</label>
            <el-input
              id="email"
              v-model="email"
              type="email"
              autocomplete="email"
              placeholder="anna@gmail.com"
              @focus="isTyping = true"
              @blur="isTyping = false"
              class="h-12"
              clearable
            />
          </div>

          <div class="space-y-2">
            <label for="password" class="text-sm font-medium leading-none">Password</label>
            <el-input
              id="password"
              v-model="password"
              :type="showPassword ? 'text' : 'password'"
              autocomplete="current-password"
              placeholder="••••••••"
              class="h-12"
              @focus="isTyping = true"
              @blur="isTyping = false"
            >
              <template #suffix>
                <span
                  class="cursor-pointer text-muted-foreground hover:text-foreground transition-colors"
                  @click="showPassword = !showPassword"
                >
                  <svg v-if="showPassword" xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M9.88 9.88a3 3 0 1 0 4.24 4.24"/>
                    <path d="M10.73 5.08A10.43 10.43 0 0 1 12 5c7 0 10 7 10 7a13.16 13.16 0 0 1-1.67 2.68"/>
                    <path d="M6.61 6.61A13.526 13.526 0 0 0 2 12s3 7 10 7a9.74 9.74 0 0 0 5.39-1.61"/>
                    <line x1="2" x2="22" y1="2" y2="22"/>
                  </svg>
                  <svg v-else xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M2 12s3-7 10-7 10 7 10 7-3 7-10 7-10-7-10-7Z"/>
                    <circle cx="12" cy="12" r="3"/>
                  </svg>
                </span>
              </template>
            </el-input>
          </div>

          <div class="flex items-center justify-between">
            <el-checkbox v-model="rememberMe" label="Remember for 30 days" />
            <a href="#" class="text-sm text-primary hover:underline font-medium">
              Forgot password?
            </a>
          </div>

          <div v-if="error" class="p-3 text-sm text-red-400 bg-red-950/20 border border-red-900/30 rounded-lg">
            {{ error }}
          </div>

          <el-button
            type="primary"
            native-type="submit"
            class="w-full h-12 text-base font-medium"
            size="large"
            :disabled="isLoading || !canSubmit"
            :loading="isLoading"
          >
            {{ isLoading ? 'Signing in...' : 'Log in' }}
          </el-button>
        </form>

        <!-- Social Login -->
        <div class="mt-6">
          <el-button class="w-full h-12 bg-background border-border/60 hover:bg-accent" native-type="button">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-2">
              <rect width="20" height="16" x="2" y="4" rx="2"/>
              <path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/>
            </svg>
            Log in with Google
          </el-button>
        </div>

        <!-- Sign Up Link -->
        <div class="text-center text-sm text-muted-foreground mt-8">
          Don't have an account?
          <a href="#" class="text-foreground font-medium hover:underline">
            Sign Up
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'
import { ElMessage } from 'element-plus'
import AnimatedCharacters from './AnimatedCharacters.vue'

const showPassword = ref(false)
const email = ref('')
const password = ref('')
const error = ref('')
const isLoading = ref(false)
const isTyping = ref(false)
const rememberMe = ref(false)
const loginErrorTick = ref(0)

const normalizedEmail = computed(() => email.value.trim().toLowerCase())
const canSubmit = computed(() => normalizedEmail.value.length > 0 && password.value.length > 0)

const handleSubmit = async () => {
  error.value = ''

  if (!canSubmit.value) {
    error.value = 'Please enter both email and password.'
    return
  }

  isLoading.value = true

  await new Promise((resolve) => setTimeout(resolve, 300))

  if (normalizedEmail.value === 'erik@gmail.com' && password.value === '1234') {
    ElMessage.success('Login successful! Welcome, Erik!')
  } else {
    error.value = 'Invalid email or password. Please try again.'
    loginErrorTick.value += 1
  }

  isLoading.value = false
}
</script>

<style scoped>
.bg-grid-white\/\[0\.05\] {
  background-image: linear-gradient(to right, rgba(255, 255, 255, 0.05) 1px, transparent 1px),
                    linear-gradient(to bottom, rgba(255, 255, 255, 0.05) 1px, transparent 1px);
  background-size: 20px 20px;
}
</style>