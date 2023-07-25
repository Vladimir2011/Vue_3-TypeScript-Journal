<script setup lang="ts">
import TheHeader from '@/components/TheHeader.vue'
import EntryEditor from './components/EntryEditor.vue'
import EntryCard from '@/components/EntryCard.vue'
import { reactive, provide } from 'vue'
import { userInjectionKey } from '@/injectionsKeys'
import type User from '@/types/User'
import type Entry from '@/types/Entry'

const entries: Entry[] = reactive([
  {
    body: 'I had a great time with my friends',
    emoji: 'happy',
    createdAt: new Date(),
    userId: 1,
    id: 3.54
  }
])
const user: User = reactive({
  id: 1,
  username: 'Vladimir',
  settings: []
})
provide(userInjectionKey, user)

const handleCreateEntry = (entry: Entry) => {
  entries.unshift(entry)
}
</script>

<template>
  <main class="container m-auto p-10">
    <TheHeader />
    <EntryEditor @@create="handleCreateEntry" />
    <ul>
      <li v-for="entry in entries" :key="entry.id">
        <EntryCard :entry="entry" />
      </li>
    </ul>
  </main>
</template>
