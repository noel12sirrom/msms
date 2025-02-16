<script lang="ts">
	import Header from './Header.svelte';
	import '../app.css';

	let { children } = $props();
</script>

<div class="bg-[url('$lib/images/background.jpg')] bg-cover bg-center min-h-screen flex flex-row min-h-screen">
	<Header />

	<main >
		{@render children()}
	</main>

</div>

<style>

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		
		margin: 0 auto;
		box-sizing: border-box;
		justify-content: center;
		align-items: center;
	}


	@media (min-width: 480px) {
		footer {
			padding: 12px 0;
		}
	}
</style>
