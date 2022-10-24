<script setup lang="ts">
import type { QueryBuilderParams } from '@nuxt/content/dist/runtime/types'
// const Tui = () => (process.client ? import ('~/components/content/Tui.client.vue') : Promise.resolve({ render: (h) => ('div')}))
// import Tui from '~/components/content/Tui.client.vue'
// const Tui = () => process.client ? import('~/components/content/Tui.client.vue') : null
const Tui = defineAsyncComponent(() => import('~/components/content/Tui.client.vue'))
const query: QueryBuilderParams = { path: '/exchanges', where: { layout: 'index' }, limit: 5, sort: { createdAt: -1 } }
</script>
<template>
  <main>
    <ContentList :query="query" v-slot="{ list }">
      <div v-for="article in list" :key="article._path">
        <h2>{{ article.title }}</h2>
        <p>{{ article.description }}</p>
      </div>
    </ContentList>
    <ClientOnly>
      <Tui />
    </ClientOnly>
  </main>
</template>