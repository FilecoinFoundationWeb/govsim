<script>
	import { onMount } from "svelte";
	import { Styles } from '@sveltestrap/sveltestrap';
	/**
	 * @type {HTMLElement}
	 */
	let el;

	import Slider from "$lib/Slider.svelte";

	onMount(async () => {
	  const { createEditor } = await import("../lib/editor");
	  createEditor(el);
	});
</script>

<main>
	<Styles />
	<Slider />
	<div class="rete" bind:this={el} />

</main>


<style>
	.rete {
	  position: relative;
	  width: 100vw;
	  height: 100vh;
	  font-size: 1rem;
	  text-align: left;
	  border: 1px solid #cbd0db;
	}

	:global(body) {
	  margin: 0;
	  overflow: hidden;
	}
</style>
