<script>
  import { query } from "svelte-apollo";
  import { gql } from "@apollo/client/core";

  const GET_MOVIES = gql`
    query Movies {
      movies(first: 10) {
        federateMovie {
          data {
            Title
            Poster
            Genre
            Director
          }
        }
        id
        slug
      }
    }
  `;

  const movies = query(GET_MOVIES);
</script>

<div class="movies-container">
  {#if $movies.loading}
    Loading...
  {:else if $movies.error}
    Error: {$movies.error.message}
  {:else}
    {#each $movies.data.movies as { federateMovie: { data: movie }, id }}
      <div key={id} class="movie-card">
        <h3>{movie.Title}</h3>
        <img src={movie.Poster} alt={movie.Title} />
        <p>Genre: {movie.Genre}</p>
        <p>Director: {movie.Director}</p>
      </div>
    {/each}
  {/if}
</div>

<style>
  .movies-container {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
  }
  .movie-card {
    border: 1px solid #ccc;
    padding: 20px;
    border-radius: 8px;
  }
  img {
    width: 100%;
    max-height: 300px;
    object-fit: cover;
    border-radius: 4px;
  }
</style>
