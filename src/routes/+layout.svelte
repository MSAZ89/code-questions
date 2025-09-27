<script lang="ts">
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';
	import Topmenu from '$lib/components/topmenu.svelte';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<main class="min-h-screen bg-black p-2">
	<Topmenu />
	{@render children?.()}
</main>
