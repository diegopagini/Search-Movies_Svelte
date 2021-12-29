<!-- scripts -->
<script>
  import Movie from './Movie.svelte';

  let value = ''
  let response = []; 
  let loading = false;

  const handleInput = (event) => value = event.target.value;

  $: if(value.length > 2) {
    loading = true;
    fetch(`https://www.omdbapi.com/?s=${value}&apikey=3ea235a0`)
    .then(res => res.json())
    .then(apiResponse => {
      response = apiResponse.Search || [];
      loading = false;
    });
  }

</script>
<!-- end of scripts -->

<!-- html -->
<div class="input">
  <input 
    type="text" 
    on:input={handleInput}
    placeholder="Search movies" 
  />

  {#if loading}
    <em>loading...</em>
  {:else}
    {#each response as movie, index}
      <Movie index={index} movie={movie} />
    {:else} <!-- else of each (wow!) -->
      <p>No tenemos películas.</p>    
    {/each}  
  {/if}

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
