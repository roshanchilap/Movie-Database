<script>
	import { goto } from '$app/navigation';
	import { fly } from 'svelte/transition';

	let inputValue = '';
	let active = false;

	function cancelInactive() {
		if (inputValue) {
			active = true;
		} else {
			active = false;
		}
	}

	function submitSearch() {
		goto('/search/' + inputValue);
	}
</script>

<form on:submit|preventDefault={submitSearch} class="search">
	{#if !active}
		<label in:fly={{ y: -10, duration: 500 }} out:fly={{ y: -10, duration: 500 }} for="search_movie"
			>Search Movies</label
		>
	{/if}

	<input
		on:blur={cancelInactive}
		on:focus={() => (active = true)}
		bind:value={inputValue}
		type="text"
		name="search_movie"
		class={active ? 'selected' : ''}
	/>
	{#if inputValue}
		<button in:fly={{ x: -10, duration: 500 }} out:fly={{ x: -20, duration: 500 }}>Search</button>
	{/if}
</form>

<style>
	.search {
		position: relative;
		width: 30%;
		margin: 1rem;
	}
	button {
		font-size: 0.7rem;
		padding: 0rem 1rem;
		background-color: rgb(78 24 133);
		color: white;
		font-weight: bold;
		border: none;
		position: absolute;
		bottom: 50%;
		right: 0;
		transform: translate(0, 50%);
		height: 100%;
		border-top-right-radius: 10px;
		border-bottom-right-radius: 10px;
		cursor: pointer;
	}
	input {
		width: 100%;
		font-size: 1rem;
		padding: 0.5rem 0.1rem;
		background-color: rgb(63, 63, 63);
		color: rgb(255, 255, 255);
		font-weight: bold;
		border: none;
		transition: background 0.75s ease-out;
		border-radius: 10px;
		padding: 0.7rem;
	}
	label {
		position: absolute;
		font-size: 0.8rem;
		top: 50%;
		left: 10px;
		transform: translate(0, -50%);
		pointer-events: none;
		color: #fff;
		padding: 0rem 1 rem;
	}

	input.selected {
		background-color: rgb(50, 50, 50);
	}
</style>
