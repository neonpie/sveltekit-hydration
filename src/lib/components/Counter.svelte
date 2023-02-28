<script lang="ts">
	import { writable } from 'svelte/store';
	export let number: number;

	const count = writable(number || 0);

	const eventHandler = () => {
		document.body.style.background = 'red';
		return () => count.update((n) => n + 1);
	};
</script>

<button on:click={eventHandler()}>{$count}</button>
