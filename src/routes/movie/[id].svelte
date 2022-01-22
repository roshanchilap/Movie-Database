<script context="module">
	import { compute_slots } from 'svelte/internal';

	export async function load({ fetch, params }) {
		const response = await fetch(
			`https://api.themoviedb.org/3/movie/${params.id}?api_key=470908b22c0dc053af9fe8f0be8d636f&language=en-US&page=1`
		);
		const movieDetails = await response.json();
		if (response.ok) {
			return {
				props: { movieDetails }
			};
		}
	}
</script>

<script>
	export let movieDetails;
	import { fly } from 'svelte/transition';
</script>

<div
	class="movie-details"
	in:fly={{ y: 50, duration: 500, delay: 500 }}
	out:fly={{ duration: 500 }}
>
	<div class="img-container">
		<img
			src={'https://image.tmdb.org/t/p/original' + movieDetails.backdrop_path}
			alt={movieDetails.title}
		/>
	</div>
	<div class="txt-container">
		<h1 in:fly={{ y: 30, duration: 500, delay: 600 }} out:fly={{ duration: 500 }}>
			{movieDetails.title}
		</h1>
		<p class="overview" in:fly={{ y: 30, duration: 500, delay: 600 }} out:fly={{ duration: 500 }}>
			{movieDetails.overview}
		</p>
		<p>
			<span in:fly={{ y: 30, duration: 500, delay: 600 }} out:fly={{ duration: 500 }}
				>Release Date:
			</span>
			{movieDetails.release_date} <br />
			<span in:fly={{ y: 30, duration: 500, delay: 600 }} out:fly={{ duration: 500 }}
				>Budget:
			</span>
			${movieDetails.budget} <br />
			<span in:fly={{ y: 30, duration: 500, delay: 600 }} out:fly={{ duration: 500 }}
				>Rating:
			</span>
			{movieDetails.vote_average} <br />
			<span in:fly={{ y: 30, duration: 500, delay: 600 }} out:fly={{ duration: 500 }}
				>Runtime:
			</span>
			{movieDetails.runtime} <br />
		</p>
	</div>
</div>

<style>
	p {
		padding: 1rem 0rem;
	}
	.img-container {
		width: 100%;
	}
	img {
		width: 100%;
		border-radius: 1rem;
	}
	.movie-details {
		margin: 2rem 20%;
	}
	span {
		font-weight: bold;
	}
</style>
