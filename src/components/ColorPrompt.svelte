<script lang="ts">
  import { socket } from "../stores/session";

  const colors = ["red", "blue", "green", "yellow"];
  export let card;
  export let open;
</script>

<div class="container">
  <h2>Pick a Color</h2>
  {#each colors as clr}
    <button
      style="background-color: {clr};"
      on:click={() => {
        $socket.emit("play-card", { card, color: clr });
        open = false;
      }}
    />
  {/each}
  <div>
    <button
      on:click={() => {
        open = false;
      }}>Close</button
    >
  </div>
</div>

<style>
  .container {
    position: fixed;
    top: 5rem;
    left: 50%;
    transform: translateX(-50%);
    padding: 5rem;
    background: black;
    border-radius: 2rem;
    z-index: 10;
  }
  button {
    margin: 0.2rem;
    padding: 2rem;
  }
</style>
