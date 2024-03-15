<script lang="ts">
	import imagesLoaded from 'imagesloaded';
	import { browser } from '$app/environment';
	import Loader from '$lib/components/Loader.svelte';
	import { dictionary } from './../../.svelte-kit/generated/client/app.js';
	import Lenis from '@studio-freight/lenis/types';
	import '$lib/assets/web/inter.css';
	import '../app.pcss';
	import { navigating } from '$app/stores';
	import { onMount } from 'svelte';
	
	let loaded = false;

	onMount(() => {
		imagesLoaded('always', { background: true }, function () {
			console.log('.images background image loaded');
			loaded = true;
		});
	});
</script>

<svelte:head>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
	<link
		href="https://fonts.googleapis.com/css2?family=Kode+Mono:wght@400..700&family=Nunito+Sans:ital,opsz,wght@0,6..12,200..1000;1,6..12,200..1000&family=Satisfy&display=swap"
		rel="stylesheet"
	/>

	<link
		href="https://fonts.googleapis.com/css2?family=Josefin+Sans:ital,wght@0,100..700;1,100..700&display=swap"
		rel="stylesheet"
	/>
	<link
		href="https://fonts.googleapis.com/css2?family=Ubuntu+Mono:ital,wght@0,400;0,700;1,400;1,700&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<div id="fullpage" class=" relative font-ubuntu">
	{#if !browser || $navigating ||!loaded}
		<Loader />
	{:else}
		<slot />
	{/if}
</div>

<style>
	#fullpage::-webkit-scrollbar {
		width: 8px;
	}

	#fullpage::-webkit-scrollbar-track {
		border-radius: 8px;
		background-color: #e7e7e7;
		border: 1px solid #cacaca;
	}

	#fullpage::-webkit-scrollbar-thumb {
		border-radius: 6px;
		background-color: #3332324f;
	}
</style>
