<script>
  import { navigate } from "svelte-routing";

  export let todos; // receive todos array prop
  export let id; // receive id prop
  export let url; // receive url prop
  export let getTodos; // receive getTodos prop

  let buttonLabel = "Create Todo"; //default for submit button text
  let subject = ""; //default for subject field
  let details = ""; //default for subject field
  // default value of handle submit for creating todos
  let handleSubmit = async (event) => {
    event.preventDefault();

    await fetch(url, {
      method: "post",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        subject,
        details,
      }),
    });

    getTodos();
    navigate("/", { replace: true });
  };

  // if id is defined, reconfigure for editing
  if (id) {
    buttonLabel = "edit a todo";
    const post = todos.find((p) => p.id == id);
    subject = post.subject;
    details = post.details;
    handleSubmit = async (event) => {
      event.preventDefault();

      await fetch(url + id + "/", {
        method: "put",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          id,
          subject,
          details,
        }),
      });

      getTodos();
      navigate("/", { replace: true });
    };
  }
</script>

<div>
  <form on:submit={handleSubmit}>
    <input type="text" placeholder="subject" bind:value={subject} />
    <input type="text" placeholder="details" bind:value={details} />
    <input type="submit" bind:value={buttonLabel} />
  </form>
</div>

<style></style>
