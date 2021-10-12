<script>
  import { onMount } from "svelte";
  import { Router, Route, Link } from "svelte-routing";
  import AllPosts from "./pages/AllPosts.svelte";
  import SinglePost from "./pages/SinglePost.svelte";
  import Form from "./pages/Form.svelte";

  export let url = ""; // prop for router to url
  let todos; // variable to hold todo
  let baseURL = "https://api.herokuapp.com/todos/"; //api url

  //function to get todos
  const getTodos = async () => {
    const response = await fetch(baseURL);
    const data = await response.json();
    todos = data;
  };

  onMount(() => getTodos());
</script>

<style>
  .app {
    text-align: center;
  }
</style>

<Router url="{url}">
  <div class="app">
    <h1>Our Todos</h1>
    <main>
      <Route path="/post/:id" let:params
        ><SinglePost
          todos="{todos}"
          id="{params.id}"
          getTodos="{getTodos}"
          url="{baseURL}"
      /></Route>
      <Route path="/new"
        ><form todos="{todos}" url="{baseURL}" getTodos="{getTodos}"
      /></Route>
      <Route path="/edit/:id" let:params
        ><form
          todos="{todos}"
          id="{params.id}"
          url="{baseURL}"
          getTodos="{getTodos}"
      /></Route>
      <Route path="/"><AllPosts todos="{todos}" /></Route>
    </main>
  </div>
</Router>
