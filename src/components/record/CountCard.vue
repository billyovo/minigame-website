<template>
  <v-card
    :elevation="10"
    :width="250"
    class="pa-2"
  >
    <template #prepend>
      <NuxtImg :src="imagePath" :height="30" :width="30" />
    </template>
    <template #title>
      {{ data.name }}
    </template>
    <template #text>
      <v-row>
        <v-col cols="12" class="d-flex align-center">
          <span>勝利次數: {{ data.total }}</span>
        </v-col>
      </v-row>
    </template>
  </v-card>
</template>

<script setup lang="ts">
import type { WinnerCountItem } from '~/@types/record'

const { data } = defineProps<{data: WinnerCountItem}>()

const imagePath = computed(() => {
	if (data.UUID === 'draw_result') {
		return '/images/record/draw.png'
	} else {
		return `https://crafatar.com/avatars/${data.UUID}?overlay=true`
	}
})
</script>
