<!-- scripts -->
<script>
  import Movie from './Movie.svelte';

  let value = ''
  let response = []; 

  const handleInput = (event) => value = event.target.value;

  $: if(value.length > 2) {
    response = fetch(`https://www.omdbapi.com/?s=${value}&apikey=3ea235a0`)
    .then(res => !res.ok() && new Error('Somenthing bad happened with the fetching of movies.'))
    .then(res => res.json())
    .then(apiResponse => apiResponse.Search || []);
  }
</script>
<!-- end of scripts -->

<!-- html -->
<div class="input">
  <input 
    type="text" 
    on:input={handleInput}
    placeholder="Search yout movies..." 
  />

  {#await response}
    <em>loading...</em>
  {:then movies}
    {#each movies as movie, index}
      <Movie index={index} movie={movie} />
    {:else} <!-- else of each (wow!) -->
      <p>No tenemos películas.</p>    
    {/each}  
  {:catch error}
    <p>There has been an error.</p>
  {/await}

</div>
<!--end of html -->

<!-- styles -->
<style>
  .input {
    align-items: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 100%;
  }

</style>
<!-- end of styles -->
