<script>
	import Header from "$lib/header.svelte";
	import "../styles/reset.css";
	import "../styles/main.css";
</script>

<Header />

<main>
	<slot />
</main>

<footer>
	<!-- <p>Footer</p> -->
</footer>

<style>
	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		max-width: 1024px;
		margin: 0 auto;
		box-sizing: border-box;
		padding-top: 2.5rem;
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 40px;
	}

	@media (min-width: 480px) {
		footer {
			padding: 40px 0;
		}
	}
</style>
