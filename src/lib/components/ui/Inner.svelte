<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	function sayHello() {
		dispatch('custom', {
			text: 'hello'
		});
	}
</script>

<button on:click={sayHello}> Click to say hello </button>
