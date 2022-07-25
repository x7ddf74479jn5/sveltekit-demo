<script context="module" lang="ts">
	import type { Load } from '@sveltejs/kit';
	import type { Post } from 'src/types';

	export const load: Load = async ({ fetch, params }) => {
		const response = await fetch(`https://jsonplaceholder.typicode.com/posts/${params.slug}`);
		const post = (await response.json()) as Post;
		return {
			props: {
				post: response.ok && post
			}
		};
	};
</script>

<script lang="ts">
	export let post: Post;
</script>

<div class="post">
	<h2>{post.title}</h2>
	<p>{post.body}</p>
</div>

<style>
	.post {
		padding: 10px;
	}
</style>