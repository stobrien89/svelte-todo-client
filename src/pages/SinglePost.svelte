<script>
  import { Link } from "svelte-routing";
  // gets posts and id props
  export let todos;
  export let id;
  export let getTodos; // receive getTodos as props
  export let url; // get url as prop

  const post = todos.find((p) => p.id == id);
</script>

<div>
  <h1>{post.subject}</h1>
  <h2>{post.details}</h2>
  <Link to="/"><button>Back to Main</button></Link>
  <Link to={"/edit/" + post.id}><button>Edit the Todo</button></Link>
</div>

<style>
</style>
