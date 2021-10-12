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
    try {
      const response = await fetch(baseURL);
      const data = await response.json();
      todos = data;
    } catch (err) {
      console.error(err);
    }
  };

  onMount(() => getTodos());
</script>

<Router {url}>
  <div class="app">
    <h1>Our Todos</h1>
    <main>
      <Route path="/post/:id" let:params
        ><SinglePost {todos} id={params.id} {getTodos} url={baseURL} /></Route
      >
      <Route path="/new"><form {todos} url={baseURL} {getTodos} /></Route>
      <Route path="/edit/:id" let:params
        ><form {todos} id={params.id} url={baseURL} {getTodos} /></Route
      >
      <Route path="/"><AllPosts {todos} /></Route>
    </main>
  </div>
</Router>

<style>
  .app {
    text-align: center;
  }
</style>
