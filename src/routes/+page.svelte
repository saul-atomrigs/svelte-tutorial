<script>
	import Nested from '$lib/components/ui/Nested.svelte';
	import Inner from '$lib/components/ui/Inner.svelte';
	import Outer from '$lib/components/ui/Outer.svelte';
	import { getRandomNumber } from '../lib/utils.js';

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

	const colors = ['red', 'green', 'blue'];
	let selected = colors[0];

	let promise = getRandomNumber();

	function handleClick() {
		promise = getRandomNumber();
	}

	let m = { x: 0, y: 0 };
	function handleMove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}

	let yes = false

	let questions = [
		{
			id: 1,
			text: `What's your name?`,
		},
		{
			id: 2,
			text: `How old are you?`,
		},
		{
			id: 3,
			text: `What's your email?`,
		}
	]

	let answer = ''

	function handleSubmit() {
		alert(answer)
	}
</script>

<form on:submit|preventDefault={handleSubmit}>
	<select bind:value={selected} on:change={()=>(answer='')}>
		{#each questions as question}
			<option value={question.id}>
				{question.text}
			</option>
		{/each}
	</select>

	<input bind:value={answer}>

	<button disabled={!answer} type='submit'>
		Submit
	</button>
</form>

<input type="text" bind:value={name}>
<input type="number" bind:value={name}>

<label>
	<input type="checkbox" bind:checked={yes}>
	Send me email
</label>

{#if yes}
	<p>Yes</p>
{:else}
	<p>No</p>
{/if}



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

{#if count > 5}
	<p>count is greater than 5</p>
{:else}
	<p>count is not greater than 5</p>
{/if}

<div>
	{#each colors as color, i}
		<button
			aria-current={selected === { color }}
			aria-label={color}
			style="background:{color}"
			on:click={() => (selected = { color })}
		>
			{i + 1}
		</button>
	{/each}
</div>
<p>{count} doubled is {doubled}</p>

<p>{numbers.join(' + ')} = {sum}</p>
<button on:click={addNumber}> Add a number </button>

<button on:click={handleClick}> Get Random Number </button>

{#await promise}
	<p>waiting...</p>
{:then number}
	<p>{number}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}

<div on:pointermove={handleMove}>
	The pointer is at {m.x}
	{m.y}
</div>

<button on:click|once={() => alert('hello')}> Click </button>

<Inner on:custom={(event) => alert(event.detail.text)} />

<Outer />

<style>
	p {
		color: red;
	}
</style>
