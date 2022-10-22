<template>
  <div>
  <slot />
  <div v-for="post in posts" :key="post._path">
    <img class="aspect-video object-cover object-center" :src="post.image" :alt="post.title" />
    <NuxtLink :to="post._path">
      <h2>{{ post.title }}</h2>
    </NuxtLink>
    <p>{{ post.description }}</p>
  </div>
  </div>
</template>
<script setup>
// using nuxt useAsyncData composable to query
const { data: posts } = await useAsyncData("posts", () => {
  return queryContent("exchanges/bitget")
  .where({ _path: { $ne: "/exchanges/bitget" } })  // exclude content/blog/index.md
  .sort({ createdAt: -1 }) // sort by createdAt desc
  .only(['title','image','_path','description']) // only select these fields
      .find();
});
console.log(posts)
</script>