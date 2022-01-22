<script context="module">
	import { compute_slots } from 'svelte/internal';

	export async function load({ fetch }) {
		const response = await fetch(
			'https://api.themoviedb.org/3/movie/popular?api_key=470908b22c0dc053af9fe8f0be8d636f&language=en-US&page=1'
		);
		const data = await response.json();
		if (response.ok) {
			return {
				props: { popular: data.results }
			};
		}
	}
</script>

<script>
	import PopularMovies from '../components/PopularMovies.svelte';
	import SearchMovies from '../components/SearchMovies.svelte';
	export let popular;
	import { fly } from 'svelte/transition';
</script>

<section in:fly={{ y: 50, duration: 500, delay: 500 }} out:fly={{ duration: 500 }}>
	<SearchMovies />
	<PopularMovies {popular} />
</section>
