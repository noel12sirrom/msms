<script lang="ts">
	import { page } from '$app/state';
	import logo from '$lib/images/ms-logo.jpg';
	import github from '$lib/images/github.svg';

	let pages ={
		Employee: '/employee',
		Inventory: '/inventory',
		Orders: '/orders',
		Repairs: '/repairs',
		Reports: '/reports'
	}
</script>

<header class="border-r w-1/6 border-gray-200 flex flex-col items-center justify-between bg-gray-200">
	<div class="w-[3em] h-[3em]">
		<a href='/'>
			<img src={logo} alt="SvelteKit" />
		</a>
	</div>


	<nav class="w-full">
		<ul class="flex flex-col justify-between items-center w-full border-2">
			{#each Object.keys(pages) as pageName, i}
			<li class="w-full text-center p-5 
			{page.url.pathname === pages[pageName] ? 'bg-none' : 'text-gray-700'}" 
			aria-current={page.url.pathname === pages[pageName] ? 'page' : undefined}>
				<a href={pages[pageName]}>{pageName}</a>
			</li>
			{/each}
		</ul>
	</nav>
	<div>
		<h1>Motorcycle Managment System</h1>
	</div>

</header>

<style>


</style>
