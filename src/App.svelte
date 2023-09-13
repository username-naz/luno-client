<script lang="ts">
  import { Router, Link, Route } from "svelte-routing";
  import Home from "./pages/Home.svelte";
  import Game from "./pages/Game.svelte";

  export let url = "";
  let socket;
</script>

<Router {url}>
  <div>
    <Route path="/"><Home {socket} /></Route>
    <Route path="/game"><Game /></Route>
  </div>
</Router>
