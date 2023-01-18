<script>
	export let highScore;
	export let newHighscore;
</script>

<div>
	<div>Highscore</div>
	<div class="text-4xl p-3 font-semibold">{highScore}</div>
	{#if newHighscore}
		<div class="text-pink-500 text-1xl">Nieuwe highscore!!</div>
	{/if}
</div>
