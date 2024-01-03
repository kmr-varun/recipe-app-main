
<svelte:head>
	<title>Recipe App</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<script>

let formData = {
    name: '',
    tagline: '',
    ingredients: '',
    instructions: ''
};

/**
 * @type {string}
 */
let recipeStat = "Error";

async function sendData() {
  try {
    recipeStat = "Error";
    const response = await fetch('https://recipe-backend-omega.vercel.app/data/set', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(formData),
    });
    console.log(response);

    if (response.ok) {
      recipeStat = "Success";
      console.log('Data sent successfully');
    } else {
      recipeStat = "Error";
      console.error('Failed to send data');
    }
  } catch (error) {
    console.error('Error sending data:', error);
  }
}

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
  <form on:submit|preventDefault="{sendData}">
  <section class="text-gray-400 bg-gray-900 body-font relative">
    <div class="container px-5 py-24 mx-auto">
      <div class="flex flex-col text-center w-full mb-12">
        <h1 class="sm:text-3xl text-2xl font-medium title-font mb-4 text-white">Add Recipe</h1>
      </div>
      <div class="lg:w-1/2 md:w-2/3 mx-auto">
        <div class="flex flex-wrap -m-2">
          <div class="p-2 w-1/2">
            <div class="relative">
              <label for="name" class="leading-7 text-sm text-gray-400">Name</label>
              <input type="text" id="name" name="name" class="w-full bg-gray-800 bg-opacity-40 rounded border border-gray-700 focus:border-indigo-500 focus:bg-gray-900 focus:ring-2 focus:ring-indigo-900 text-base outline-none text-gray-100 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out" bind:value={formData.name}>
            </div>
          </div>
          <div class="p-2 w-1/2">
            <div class="relative">
              <label for="tagline" class="leading-7 text-sm text-gray-400">TagLine</label>
              <input type="text" id="tagline" name="tagline" class="w-full bg-gray-800 bg-opacity-40 rounded border border-gray-700 focus:border-indigo-500 focus:bg-gray-900 focus:ring-2 focus:ring-indigo-900 text-base outline-none text-gray-100 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out" bind:value={formData.tagline}>
            </div>
          </div>


          
          <div class="p-2 w-full">
            <div class="relative">
              <label for="ingredients" class="leading-7 text-sm text-gray-400">Ingredients</label>
              <textarea id="ingredients" name="ingredients" class="w-full bg-gray-800 bg-opacity-40 rounded border border-gray-700 focus:border-indigo-500 focus:bg-gray-900 focus:ring-2 focus:ring-indigo-900 h-32 text-base outline-none text-gray-100 py-1 px-3 resize-none leading-6 transition-colors duration-200 ease-in-out" bind:value={formData.ingredients}></textarea>
            </div>
          </div>
          <div class="p-2 w-full">
            <div class="relative">
              <label for="instructions" class="leading-7 text-sm text-gray-400">Instructions</label>
              <textarea id="instructions" name="instructions" class="w-full bg-gray-800 bg-opacity-40 rounded border border-gray-700 focus:border-indigo-500 focus:bg-gray-900 focus:ring-2 focus:ring-indigo-900 h-32 text-base outline-none text-gray-100 py-1 px-3 resize-none leading-6 transition-colors duration-200 ease-in-out" bind:value={formData.instructions}></textarea>
            </div>
          </div>
          {#if recipeStat == "Success"}
              Recipe Added Succesfully
          {/if}
          <div class="p-2 w-full">
            <button type="submit" class="flex mx-auto text-white bg-indigo-500 border-0 py-2 px-8 focus:outline-none hover:bg-indigo-600 rounded text-lg">Add</button>
          </div>
        </div>
      </div>
    </div>
  </section>
</form>



