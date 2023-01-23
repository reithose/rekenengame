<script>
	import { onMount, createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	let firstNumber;
	let secondNumber;
	let rightAnswer;
	let userAnswer;
	let validityAnswer;
	let somTypeSymbol;

	let newMultiplySom;
	let newAddSom;
	let newSubstractSom;

	const somTypeFunctions = [
		(newMultiplySom = () => {
			somTypeSymbol = '×';
			firstNumber = Math.floor(Math.random() * 5);
			secondNumber = Math.floor(Math.random() * 5);
			rightAnswer = firstNumber * secondNumber;
		}),
		(newAddSom = () => {
			somTypeSymbol = '+';
			firstNumber = Math.floor(Math.random() * 100);
			secondNumber = Math.floor(Math.random() * 10);
			rightAnswer = firstNumber + secondNumber;
		}),
		(newSubstractSom = () => {
			somTypeSymbol = '-';
			firstNumber = Math.floor(Math.random() * 20);
			secondNumber = Math.floor(Math.random() * firstNumber); //Tweede nummer is altijd lager dan het eerste nummer om een negatieve uitkomst te voorkomen.
			rightAnswer = firstNumber - secondNumber;
		})
	];

	export const newSom = () => {
		userAnswer = '';
		somTypeFunctions[Math.floor(Math.random() * somTypeFunctions.length)]();
	};

	onMount(() => {
		newSom();
	});

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
	<div>{somTypeSymbol}</div>
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
