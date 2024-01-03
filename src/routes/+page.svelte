
<svelte:head>
	<title>Recipe App</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<script>
import { onMount } from 'svelte';

/**
 * @type {any[]}
 */
let data = [];

onMount(async () => {
	const response = await fetch('https://recipe-backend-omega.vercel.app/data/get');
	const jsonData = await response.json();
	data = jsonData;
});


</script>
	
<header class="text-gray-400 bg-gray-900 body-font">
<div class="container mx-auto mt-10 flex flex-wrap p-5 flex-col md:flex-row items-left">
	<a href="/" class="flex title-font font-medium items-center text-white mb-4 md:mb-0">
	
	<span class="ml-1 text-2xl">Recipe App</span>
	</a>
	<nav class="md:ml-auto md:mr-auto flex flex-wrap items-center text-base justify-center">
	
	</nav>
	<a href="/add" class="inline-flex items-center bg-gray-800 border-0 py-3 px-4 focus:outline-none hover:bg-gray-700 rounded text-base mt-4 md:mt-0">Add Recipe
	</a>
	
</div>
</header>
{#if data}
<section class="text-gray-400 bg-gray-900 body-font">
<div class="container px-5 py-16 mx-auto">

	<div class="flex flex-wrap sm:-m-4 -mx-4 -mb-10 -mt-4">

	{#each data as recipe, i}
	<div class="p-4 md:w-1/3 sm:mb-0 mb-6">
		<div class="rounded-lg h-64 overflow-hidden">
		{#if recipe.image == undefined}
		<img alt="content" class="object-cover object-center h-full w-full" src="dummy.jpg">
		{:else}
		<img alt="content" class="object-cover object-center h-full w-full" src="{recipe.image}">
		{/if}
		</div>
		<h2 class="text-xl font-medium title-font text-white mt-5">{recipe.name}</h2>
		<p class="text-base leading-relaxed mt-2">{recipe.tagline}</p>
		<a href="/{i}" class="text-indigo-400 inline-flex items-center mt-3">View Recipe
		<svg fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" class="w-4 h-4 ml-2" viewBox="0 0 24 24">
			<path d="M5 12h14M12 5l7 7-7 7"></path>
		</svg>
		</a>
	</div>   
	{/each}
	</div>
</div>
</section>  
{/if}
