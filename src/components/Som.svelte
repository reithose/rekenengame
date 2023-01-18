<script>
	import { onMount, createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	let firstNumber;
	let secondNumber;
	let rightAnswer;
	let userAnswer;
	let validityAnswer;

	onMount(() => {
		newSom();
	});

	export const newSom = () => {
		userAnswer = '';
		firstNumber = Math.floor(Math.random() * 100);
		secondNumber = Math.floor(Math.random() * 10);
		rightAnswer = firstNumber + secondNumber;
	};

	const checkAnswer = (event) => {
		if (userAnswer) {
			if (event.key === 'Enter') {
				if (rightAnswer == userAnswer) {
					validityAnswer = true;
				} else {
					validityAnswer = false;
				}
				dispatch('handleAnswer', validityAnswer);
			}
		}
	};
</script>

<div class="grid grid-cols-auto grid-cols-5 gap-2 text-4xl">
	<div>{firstNumber}</div>
	<div>+</div>
	<div>{secondNumber}</div>
	<div>=</div>
	<div>
		<input
			class=" align-middle w-full border-b-2 border-gray-700 focus:outline-none"
			id="answer"
			name="answer"
			bind:value={userAnswer}
			on:keydown={checkAnswer}
			maxlength="3"
			autofocus
		/>
	</div>
</div>
