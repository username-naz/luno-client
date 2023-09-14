<script lang="ts">
  import type { MouseEventHandler } from "svelte/elements";
  import CardList from "../components/CardList.svelte";
  import Opponents from "../components/Opponents.svelte";
  import { data, socket } from "../stores/session";
  import CardStack from "../components/CardStack.svelte";

  const handlePickCard: MouseEventHandler<HTMLButtonElement> = () => {
    $socket.emit("pick-card");
  };
</script>

<h1>Luno</h1>

<Opponents queue={$data.game.queue} />

<br />
<CardStack cardStack={$data.game.cardStack} />
<br />
<button on:click={handlePickCard}
  ><img src="https://i.imgflip.com/60ssrg.png" alt="pick" />Pick Card</button
>
<br />
<br />
<br />
<CardList bind:cards={$data.self.cards.cardList.list} />

{#if $data.game.queue.players.find((player) => player.cards === 0)}
  <div class="winner">
    <h1>
      {$data.game.queue.players.find((player) => player.cards === 0).name} Won!
    </h1>
  </div>
{/if}

<button
  class="luno"
  on:click={() => {
    $socket.emit("call-luno");
  }}>Call Luno!</button
>

<style>
  img {
    height: 5rem;
  }

  .winner {
    position: fixed;
    padding: 10rem;
    background: black;
    border-radius: 2rem;
    color: white;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }

  .luno {
    position: fixed;
    top: 10%;
    right: 5%;
  }
</style>
