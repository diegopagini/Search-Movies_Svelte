<script>
	export let initialCounter = 0;

	let counter = initialCounter
	function handleClick () {
		counter++
	}

  $: isEvenOrOdd = counter % 2 === 0 ? 'Is Even' : 'Is Odd'

  $: {
    if(counter > 9 ){
      counter = 9
    }
  }
</script>

<main>
	<button on:click={handleClick}>Incrementar</button>
	<span>{counter}</span>
  <span>{isEvenOrOdd}</span>
</main>

<style>
	main {
		align-items: center;
		display: flex;
		flex-direction: column;
		justify-content: center;
		text-align: center;
		padding: 1em;
	
	}
</style>