<script>
	export let title;

	let colorIndex = 0;

	const colors = [
		'text-green-400',
		'text-cyan-600',
		'text-orange-600',
		'text-purple-500',
		'text-yellow-400',
		'text-red-500',
		'text-blue-500',
		'text-indigo-500',
		'text-pink-500',
		'text-lime-500',
		'text-sky-600',
		'text-fuchsia-500'
	];
	let colorClass = setInterval(() => {
		colorClass = colors[colorIndex];
		colorIndex = Math.floor(Math.random() * colors.length);
	}, 1000);
</script>

<h1 class="text-center text-5xl p-3 font-black {colorClass}">{title}</h1>
