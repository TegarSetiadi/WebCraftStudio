<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import { MAINTENANCE_MODE } from '$lib/config';
	import Maintenance from '$lib/components/Maintenance.svelte';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} type="image/svg+xml" />
</svelte:head>

{#if MAINTENANCE_MODE}
	<Maintenance />
{:else}
	{@render children()}
{/if}
