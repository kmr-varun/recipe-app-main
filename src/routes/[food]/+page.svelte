<script>

import { onMount } from 'svelte';
export let data;
const recipe  = data;
/**
* @type {any[]}
*/
let recips;

onMount(async () => {
  const response = await fetch('http://localhost:5000/data/get');
  const jsonData = await response.json();
  recips = jsonData;
});

</script>

<header class="text-gray-400 bg-gray-900 body-font">
  <div class="container mx-auto mt-10 flex flex-wrap p-5 flex-col md:flex-row items-left">
    <a href="/" class="flex title-font font-medium items-center text-white mb-4 md:mb-0">
      
      <span class="ml-1 text-2xl">Recipe App</span>
    </a>
    <nav class="md:ml-auto md:mr-auto flex flex-wrap items-center text-base justify-center">
      
    </nav>
    <a href="/" class="inline-flex items-center bg-gray-800 border-0 py-3 px-4 focus:outline-none hover:bg-gray-700 rounded text-base mt-4 md:mt-0">Back
    </a>
  </div>
</header>

{#if recips}
<section class="text-gray-400 bg-gray-900 body-font">
  <div class="container mx-auto flex px-5 py-24 md:flex-row flex-col items-center">
    <div class="lg:flex-grow md:w-1/2 lg:pr-24 md:pr-16 flex flex-col md:items-start md:text-left mb-16 md:mb-0 items-center text-center">
      <h1 class="title-font sm:text-4xl text-3xl mb-4 font-medium text-white">
          {recips[+recipe.recipe].name}
      </h1>
      <p class="mb-8 leading-relaxed">{recips[+recipe.recipe].tagline}</p>
      <div class="lg:w-2/3 flex flex-col sm:flex-row sm:items-center items-start mx-5">
          <h2 class="flex-grow sm:pr-16 text-2xl font-medium title-font text-white">Ingredients Required:</h2>
      </div>
      <ul class="mx-10 py-5 list-disc">
          {#each recips[+recipe.recipe].ingredients as ind}
              <li>{ind}</li>
          {/each}
      </ul>
      <div class="lg:w-2/3 flex flex-col sm:flex-row sm:items-center items-start mx-5">
          <h2 class="flex-grow sm:pr-16 text-2xl font-medium title-font text-white">Instructions to Prepare:</h2>
      </div>
      <ul class="mx-10 py-5 list-decimal">
          {#each recips[+recipe.recipe].instructions as ind}
              <li>{ind}</li>
          {/each}
      </ul>
    </div>
    <div class="lg:max-w-lg lg:w-full md:w-1/2 w-5/6">
      {#if recips[+recipe.recipe].image == undefined}
      <img class="object-cover object-center rounded" alt="hero" src="dummy.jpg">
      {:else}
      <img class="object-cover object-center rounded" alt="hero" src="{recips[+recipe.recipe].image}">
      {/if}
    </div>
  </div>
</section>
{:else}
<div class="flex h-screen justify-center items-center">
  <span class="loader"></span>
</div>
{/if}
