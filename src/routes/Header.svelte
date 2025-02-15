<script lang="ts">
	import { page } from '$app/state';
	import logo from '$lib/images/ms-logo.jpg';
	import github from '$lib/images/github.svg';
</script>

<header>
	<div class="corner">
		<a href='/'>
			<img src={logo} alt="SvelteKit" />
		</a>
	</div>


	<nav>
		<ul>
			<li aria-current={page.url.pathname === '/employee' ? 'page' : undefined}>
				<a href="/employee">Employee</a>
			</li>
			<li aria-current={page.url.pathname === '/inventory' ? 'page' : undefined}>
				<a href="/inventory">Inventory</a>
			</li>
			<li aria-current={page.url.pathname === '/orders' ? 'page' : undefined}>
				<a href="/orders">Orders</a>
			</li>
			<li aria-current={page.url.pathname === '/repairs' ? 'page' : undefined}>
				<a href="/repairs">Repairs</a>
			</li>
			<li aria-current={page.url.pathname === '/reports' ? 'page' : undefined}>
				<a href="/reports">Reports</a>
			</li>
		</ul>
	</nav>

</header>

<style>
	header {
		display: flex;
		justify-content: space-between;
	}

	.corner {
		width: 3em;
		height: 3em;
	}

	.corner a {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100%;
	}

	.corner img {
		width: 2em;
		height: 2em;
		object-fit: contain;
	}

	nav {
		display: flex;
		justify-content: center;
		
	}
	ul {
		position: relative;
		padding: 0;
		margin: 0;
		height: 3em;
		display: flex;
		justify-content: center;
		align-items: center;
		list-style: none;
		background: var(--background);
		background-size: contain;
	}

	li {
		position: relative;
		height: 100%;
	}

	li[aria-current='page']::before {
		--size: 6px;
		content: '';
		width: 0;
		height: 0;
		position: absolute;
		top: 0;
		left: calc(50% - var(--size));
		border: var(--size) solid transparent;
		border-top: var(--size) solid var(--color-theme-1);
	}

	nav a {
		display: flex;
		height: 100%;
		align-items: center;
		padding: 0 0.5rem;
		color: var(--color-text);
		font-weight: 700;
		font-size: 0.8rem;
		text-transform: uppercase;
		letter-spacing: 0.1em;
		text-decoration: none;
		transition: color 0.2s linear;
	}

	a:hover {
		color: var(--color-theme-1);
	}
</style>
