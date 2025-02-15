<script lang="ts">
	import welcome from '$lib/images/svelte-welcome.webp';
	import welcomeFallback from '$lib/images/svelte-welcome.png';
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<form method="post" action="/submit">
	<label for="username">
		<span>Username</span>
		<input type="text" name="username" id="username" required />
	</label>
	<br />
	<label for="password">
		<span>Password</span>
		<input type="password" name="password" id="password" required />
	</label>
	<br />
	<button type="submit">Login</button>
</form>

<style>
	form{
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	
</style>
