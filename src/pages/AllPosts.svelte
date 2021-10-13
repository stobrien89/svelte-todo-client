<script>
  import { Link } from "svelte-routing";
  export let todos = [];
</script>

<div>
  {#each todos as todo, index}
    <article>
      <Link to={"/post/" + todo.id}><h2>{todo.subject}</h2></Link>
      <h3>{todo.details}</h3>
    </article>
  {/each}
</div>

<style>
  article {
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  }
</style>
