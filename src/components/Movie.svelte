<script>
  export let index;
  export let movie;
</script>

<article class="movie">
  <h3>#{index + 1} - {movie.Title}</h3>
  <figure>
    <img src={movie.Poster} alt={movie.Title}>
    <figcaption>{movie.Year}</figcaption>
  </figure>
</article>

<style>
  .movie,
  figure {
    align-items: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
</style>