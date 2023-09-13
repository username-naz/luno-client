<script lang="ts">
  import { socket } from "../stores/session";
  export let queue;
  let audio = new Audio("/ping.mp3");
  $: if (queue.players[queue.turn].id == $socket.id) audio.play();
</script>

<div class="container">
  {#each queue.players as player, index}
    <div class="player">
      <img
        src="https://www.freeiconspng.com/thumbs/person-icon/clipart--person-icon--cliparts-15.png"
        alt="player"
      />
      <h3>{player.name}</h3>
      <h3>{player.cards} Card{player.cards > 1 ? "s" : ""} Left</h3>
      {#if queue.turn === index}
        <div class="turn">TURN</div>
      {/if}
    </div>
  {/each}
</div>
<br />

<style>
  img {
    height: 2rem;
  }
  .container {
    display: flex;
    gap: 10rem;
  }
  .player {
    background: white;
    padding: 0.5rem;
    border-radius: 0.2rem;
    color: black;
    font-size: 0.6rem;
  }
  .turn {
    color: red;
    font-size: 1.5rem;
    font-weight: 800;
  }
</style>
