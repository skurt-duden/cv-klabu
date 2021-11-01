<script>
  import { onMount } from "svelte";

  let classbooks = [];

  onMount(async () => {
    const res = await fetch(`https://jsonplaceholder.typicode.com/users`);
    classbooks = await res.json();
  });
</script>

<main>
	<h1>Klassenbücher</h1>
  {#each classbooks as cb}
    <h2 id="{cb.id}">{cb.title} <small>vom {cb.creationDate}</small></h2>
    <p>{cb.description}</p>
    {#each ["A","B", "C"] as entry}
      <ul>
         <li>{entry} <strong>{entry.title}</strong> {entry.description} <small>{entry.creationDate}</small> {entry.type} {cb.id} - {cb.name}</li>
         <li>{cb.email}</li>
     </ul>
     {:else}
      <!-- this block renders when e.length === 0 -->
        <p>loading...</p>
     {/each}
   {:else}
     <!-- this block renders when users.length === 0 -->
      <p>loading...</p>
   {/each}


</main>

<style>
  * {
    font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
      "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  }
  h1 {
    font-size: 1.4em;
    margin: 0;
    display: block;
  }
</style>