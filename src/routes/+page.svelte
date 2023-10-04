<script>
	import Nested from '$lib/components/ui/Nested.svelte';

	let name = 'Svelte';
	const src = 'https://via.placeholder.com/150';

	let string = 'this string contains some <strong>HTML</strong>';

	let count = 0;
	$: doubled = count * 2;
	function increment() {
		count++;
	}

	$: {
		console.log(`the count is ${count}`);
		console.log(`the doubled count is ${doubled}`);
	}

	$: if (count > 5) {
		alert('count is greater than 5');
	}

	let numbers = [1, 2, 3, 4];
	function addNumber() {
		numbers = [...numbers, numbers.length + 1];
	}
	$: sum = numbers.reduce((a, b) => a + b, 0);
</script>

<h1>Hello {name.toUpperCase()}</h1>

<p>This is an example</p>

<img {src} alt="placeholder" />

<Nested answer={42} />
<Nested />

<p>{@html string}</p>

<button on:click={increment}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>

<p>{count} doubled is {doubled}</p>

<p>{numbers.join(' + ')} = {sum}</p>
<button on:click={addNumber}> Add a number </button>

<style>
	p {
		color: red;
	}
</style>
