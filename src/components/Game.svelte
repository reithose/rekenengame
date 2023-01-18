<script>
	import Som from '../components/Som.svelte';
	import Countdown from './Countdown.svelte';
	import Score from './Score.svelte';
	import Highscore from './Highscore.svelte';
	import { ConfettiExplosion } from 'svelte-confetti-explosion';
	import { onMount } from 'svelte';

	let showConfetti = false;
	let showWrong = false;
	let totalScore = 0;
	let highScore;
	let newHighscore;

	let score;
	$: score;

	let newSom;
	let countdown;

	onMount(() => {
		highScore = localStorage.getItem('highScore');
		if (!highScore) highScore = 0;
	});

	const handleAnswer = (validityAnswer) => {
		if (validityAnswer.detail) {
			showConfetti = true;
			totalScore = totalScore + score;
			if (totalScore > highScore) {
				localStorage.setItem('highScore', totalScore);
				newHighscore = true;
				highScore = totalScore;
			}
			countdown.stop();
			setTimeout(() => {
				showConfetti = false;
				newSom.newSom();
				countdown.reset();
				countdown.start();
			}, 2000);
		} else {
			showWrong = true;
			totalScore = 0;
			setTimeout(() => {
				showWrong = false;
			}, 2000);
		}
	};
</script>

<div class="grid grid-cols-auto grid-cols-3 gap-2 place-content-center">
	<div class="col-span-3 mt-4"><Som on:handleAnswer={handleAnswer} bind:this={newSom} /></div>
	<div class="col-span-3 h-14 mt-4">
		{#if showConfetti}
			<div class="text-green-400 text-4xl flex justify-center">Goed 👍<ConfettiExplosion /></div>
		{/if}
		{#if showWrong}
			<div class="text-red-600 text-4xl flex justify-center">Fout ☹️</div>
		{/if}
	</div>
	<div class="col-span-1 mt-8"><Countdown bind:this={countdown} bind:seconds={score} /></div>
	<div class="col-span-1 mt-8"><Score {totalScore} /></div>
	<div class="col-span-1 mt-8"><Highscore {newHighscore} {highScore} /></div>
</div>
