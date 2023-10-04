<script>
	import Nested from '$lib/components/ui/Nested.svelte';

	let name = 'Svelte';
	const src = 'https://via.placeholder.com/150';

	let string = 'this string contains some <strong>HTML</strong>';
</script>

<h1>Hello {name.toUpperCase()}</h1>

<p>This is an example</p>

<img {src} alt="placeholder" />

<Nested />

<p>{@html string}</p>

<style>
	p {
		color: red;
	}
</style>
