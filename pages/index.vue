<template>
  <div>
    <div
      v-for="item in list.data"
      :key='item.id'
    >
      <nuxt-link
        :to="{ name: 'test-slug', params: { slug: [item.item] } }"
      >
       {{ item.item }} [ok]
      </nuxt-link>
    </div>
  </div>
</template>

<script setup lang="ts">
import { definePageMeta } from '#imports'
import {
  computed,
  //onMounted,
  onUnmounted,
  ref
} from 'vue'

import { useListStore } from '~/store/list.store'

definePageMeta({
  title: 'Home page'
})

const listStore = useListStore()

const $i18n = useTranslator()

const list = computed<IList>(() => {
  return {
    data: listStore.getListByType('test')
  }
})

const update = async (): Promise<void> => {
  await listStore.updateList({
    element: 'test'
  })
}

// onMounted (async () => {
  await listStore.initiateList({
    element: 'test',
  })

  await update()
// })
</script>

<style>
</style>
