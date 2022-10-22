<template>
	<div
        class="py-10 m-auto bg-white sm:px-8 sm:shadow dark:bg-gray-800 sm:rounded"
    >
        <main
            class="max-w-2xl px-4 mx-auto prose sm:px-8 prose-gray dark:prose-invert"
        >
		// loading image from public directory
		<img :src="`/${page.image}`" :alt="page.title" class="aspect-video" />

		// Post content 
		<slot/>

			<div class="flex justify-between items-center">
				// Prevent showing content/blog/index.md route
				// Previous Post Link 
				<NuxtLink v-if="prev && prev._path != '/exchanges/bitget'" :to="prev._path">
					{{ prev.title }}
				</NuxtLink>
				<div v-else></div>
				// Next Post Link
				<NuxtLink v-if="next" :to="next._path">
					{{ next.title }}
				</NuxtLink>
				<div v-else></div>
			</div>
        </main>
    </div>
</template>
<script setup>
// get page data from useContent composable
const { next, prev, page } = useContent(); 
</script>