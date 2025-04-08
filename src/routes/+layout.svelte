<script lang="ts">
	import { page } from '$app/state';
	import '../app.css';

	let { children } = $props();

	let paths = [
		{
			href: '/',
			name: 'Home'
		},
		{
			href: '/about',
			name: 'About'
		}
	];
</script>

<nav class="h-fit w-full bg-zinc-800">
	<div
		class="mx-auto flex h-fit w-full max-w-7xl flex-row items-center justify-between p-4 text-white"
	>
		<a href="/" class="flex flex-col">
			<div class="text-3xl">newlyn tides</div>
			<div class="text text-zinc-300">my tide predictions for newlyn</div>
		</a>
		<div class="flex flex-row gap-4">
			{#each paths as path}
				<a
					href={path.href}
					class={page.url.pathname == path.href ? 'text-blue-300' : 'hover:text-blue-300'}
					>{path.name}</a
				>
			{/each}
		</div>
	</div>
</nav>

{@render children()}
