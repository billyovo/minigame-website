<script setup lang="ts">
import { useDisplay, useTheme } from 'vuetify'
import { useApplicationStateStore } from '~/stores/state.store'

const display = useDisplay()
const theme = useTheme()
const stateStore = useApplicationStateStore()
const { isSwipingDown } = storeToRefs(stateStore)

function toggleTheme () {
	theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark'
}

const themeIcon = computed(() => {
	return theme.global.current.value.dark ? 'mdi:mdi-white-balance-sunny' : 'mdi:mdi-moon-waning-crescent'
})

defineProps({
	transparent: {
		type: Boolean,
		default: false
	}
})

</script>
<template>
  <v-app-bar
    rounded
    :elevation="0"
    :color="(transparent || display.mobile.value) ? 'transparent' : theme.current.value.colors.primary"
  >
    <v-app-bar-title v-if="!display.mobile.value">
      <NuxtLink to="/">
        <NuxtImg src="/images/logo/brand.svg" :height="50" class="py-2" />
      </NuxtLink>
    </v-app-bar-title>
    <v-spacer />

    <NuxtLink v-if="!display.mobile.value" to="/introduction" class="text-decoration-none text-white">
      <v-btn size="x-large">
        活動介紹
      </v-btn>
    </NuxtLink>

    <NuxtLink v-if="!display.mobile.value" to="/news" class="text-white">
      <v-btn size="x-large">
        通知
      </v-btn>
    </NuxtLink>

    <NuxtLink v-if="!display.mobile.value" to="/calendar" class="text-white">
      <v-btn size="x-large">
        時間表
      </v-btn>
    </NuxtLink>

    <NuxtLink v-if="!display.mobile.value" to="/record" class="text-white">
      <v-btn size="x-large">
        優勝記錄
      </v-btn>
    </NuxtLink>
    <v-btn>
      <v-icon size="x-large" :icon="themeIcon" @click="toggleTheme" />
    </v-btn>
  </v-app-bar>

  <Transition name="fade">
    <v-bottom-navigation
      v-show="isSwipingDown && display.mobile.value"
      grow
      rounded
      :bg-color="theme.current.value.colors.primary"
    >
      <NuxtLink to="/introduction" :style="{ color: 'white' }">
        <v-btn>
          <v-icon size="large" icon="mdi:mdi-text-box-outline" />
          <span> 活動介紹</span>
        </v-btn>
      </NuxtLink>

      <NuxtLink to="/news" :style="{ color: 'white' }">
        <v-btn>
          <v-icon size="large" icon="mdi:mdi-bell" />
          <span>通知</span>
        </v-btn>
      </NuxtLink>

      <NuxtLink to="/" :style="{ color: 'white' }">
        <v-btn>
          <v-icon size="large" icon="mdi:mdi-home" />
          <span>首頁</span>
        </v-btn>
      </NuxtLink>

      <NuxtLink to="/calendar" :style="{ color: 'white' }">
        <v-btn>
          <v-icon size="large" icon="mdi:mdi-calendar" />
          <span>時間表</span>
        </v-btn>
      </NuxtLink>

      <NuxtLink to="/record" :style="{ color: 'white' }">
        <v-btn>
          <v-icon size="large" icon="mdi:mdi-trophy" />
          <span>優勝記錄</span>
        </v-btn>
      </NuxtLink>
    </v-bottom-navigation>
  </Transition>
</template>
