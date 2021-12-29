<!-- scripts -->
<script>
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
    {#if response.length > 0}
      <p>Tenemos <strong>{response.length}</strong> películas.</p>
    {:else} 
      <p>No tenemos películas.</p>
    {/if}  
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
