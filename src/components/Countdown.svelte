<script>
	import { onMount, onDestroy } from 'svelte';

	export let seconds = 20;
	let intervalId;
	let animate;

	$: animate;

	export const reset = () => {
		animate = false;
		seconds = 20;
	};

	export const start = () => {
		intervalId = setInterval(() => {
			if (seconds > 1) {
				seconds--;
			}
		}, 1000);
	};

	export const stop = () => {
		clearInterval(intervalId);
		animate = true;
	};

	onMount(() => {
		start();
	});

	onDestroy(() => {
		clearInterval(intervalId);
	});
</script>

<div>
	<div>Nog</div>
	<div
		class="text-3xl p-3 font-semibold"
		class:animate-flash={animate}
		class:animate-fast={animate}
		class:text-red-500={animate}
	>
		{seconds}
	</div>
	<div>punten te verdienen voor deze som.</div>
</div>
