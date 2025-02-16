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

<header class=" w-1/6 flex flex-col items-center justify-between bg-slate-200/50 rounded-r-[5%]">
	<div class="w-[21em] h-[9em] flex items-center justify-center flex-col">
		<a href='/'>
			<img src={logo} alt="SvelteKit" />
		</a>
		<p class="-mt-12 font-bold">Hewitt's Motorcycles</p>
	</div>


	<nav class="w-full">
		<ul class="flex flex-col justify-between items-center w-full">
			{#each Object.keys(pages) as pageName, i}
			<li class=" w-full text-center p-8 text-mono font-bold hover:text-orange-500 transition duration-200 
			{page.url.pathname === pages[pageName] ? 'bg-transparent' : 'text-gray-700'}" 
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
