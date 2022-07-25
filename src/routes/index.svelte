<script context="module" lang="ts">
	import type { Load } from '@sveltejs/kit';
	import type { Post } from 'src/types';

	export const load: Load = async ({ fetch }) => {
		const response = await fetch('https://jsonplaceholder.typicode.com/posts');
		const posts = (await response.json()) as Post[];
		return {
			props: {
				posts: response.ok && posts
			}
		};
	};
</script>

<script lang="ts">
	export let posts: Post[];
</script>

<ul class="post-list">
	{#each posts as post}
		<li><a href={`posts/${post.id}`} class="post-link">{post.title}</a></li>
	{/each}
</ul>

<style>
	.post-list {
		list-style-type: decimal;
	}

	.post-list > li {
		margin-top: 10px;
	}

	.post-link {
		color: #000;
		text-decoration: none;
	}

	.post-link:hover {
		text-decoration: underline;
	}
</style>