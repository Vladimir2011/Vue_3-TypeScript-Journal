<script lang="ts" setup>
import DateDisplay from './DateDisplay.vue'
import UseEmojis from '@/composables/UseEmojis'
import type Entry from '@/types/Entry'
import { inject } from 'vue'
import { userInjectionKey } from '@/injectionsKeys'
const { findEmoji } = UseEmojis()
interface Props {
  entry: Entry
}
const props = defineProps<Props>()
const user = inject(userInjectionKey)
</script>
<template>
  <div class="entry-card">
    <div class="entry-card-body">
      <component width="75" :is="findEmoji(props.entry.emoji)"></component>
      <div class="entry-text">{{ props.entry.body }}</div>
    </div>
    <div class="entry-footer">
      <DateDisplay :date="props.entry.createdAt" class="mr-2" />
      |
      <span class="ml-2">{{ user?.username || 'Anonymous' }}</span>
    </div>
  </div>
</template>
