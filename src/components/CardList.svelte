<script lang="ts">
  import { socket } from "../stores/session";
  import ColorPrompt from "./ColorPrompt.svelte";

  export let cards;
  let wildCard;
  let pickColor = false;
  const handleCardClick = (card: any) => {
    if (card.type === "wild") {
      pickColor = true;
      wildCard = card;
      return;
    }
    $socket.emit("play-card", { card });
  };
</script>

{#if pickColor}
  <ColorPrompt card={wildCard} bind:open={pickColor} />
{/if}
<div class="container">
  {#each cards as card}
    <div
      on:click={() => {
        handleCardClick(card);
      }}
      role="button"
      tabindex="-1"
      on:keypress={() => {}}
      class="card {card.type} {card.color} {card.subType}"
    >
      <span class="center">
        {#if card.number !== undefined}
          {card.number}
        {/if}
        {#if card.type == "action"}
          {#if card.subType == "reverse"}
            ⟲
          {/if}
          {#if card.subType == "draw_two"}
            +2
          {/if}
          {#if card.subType == "skip"}
            ⦸
          {/if}
        {/if}
        {#if card.type == "wild"}
          <div class="blocks">
            <div class="red block" />
            <div class="green block" />
            <div class="yellow block" />
            <div class="blue block" />
          </div>
        {/if}
      </span>
      <span class="topLeft">
        {#if card.number !== undefined}
          {card.number}
        {/if}
        {#if card.type == "wild"}
          {#if card.subType == "draw_four"}
            +4
          {/if}
          {#if card.subType == "wild"}
            Wild
          {/if}
        {/if}
      </span>
      <span class="bottomRight">
        {#if card.number !== undefined}
          {card.number}
        {/if}
        {#if card.type == "wild"}
          {#if card.subType == "draw_four"}
            +4
          {/if}
          {#if card.subType == "wild"}
            Wild
          {/if}
        {/if}
      </span>
    </div>
  {/each}
</div>

<style>
  .container {
    width: 100%;
  }
  .card {
    display: inline-block;
    margin-left: -5rem;
    width: 6rem;
    height: 15rem;
    border-radius: 1rem;
    position: relative;
    background-color: white;
    cursor: pointer;
    transition: 200ms;
  }
  .card:hover {
    transform: translate(-20%, -15%) scale(105%);
  }
  .center {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-weight: 600;
    font-size: 8rem;
    aspect-ratio: 1;
    border-radius: 50%;
    background: white;
    padding: 1rem;
  }

  .draw_two .center {
    font-size: 6rem;
  }

  .topLeft {
    position: absolute;
    top: 1rem;
    left: 1rem;
    transform: translate(-50%, -50%);
    font-weight: 600;
    font-size: 2rem;
    aspect-ratio: 1;
    border-radius: 50%;
    width: 0;
    height: 0;
  }
  .bottomRight {
    position: absolute;
    bottom: 3rem;
    right: 0rem;
    transform: translate(-50%, -50%);
    font-weight: 600;
    font-size: 2rem;
    aspect-ratio: 1;
    border-radius: 50%;
    height: 0;
  }

  .wild {
    border: solid 5px white;
    background-color: black;
  }
  .red {
    color: red;
    background-color: rgb(239, 217, 217);
    border: solid 5px red;
  }
  .blue {
    color: blue;
    background-color: rgb(217, 219, 239);
    border: solid 5px blue;
  }
  .green {
    color: green;
    background-color: rgb(217, 239, 217);
    border: solid 5px green;
  }
  .yellow {
    color: rgb(199, 199, 14);
    background-color: rgb(239, 235, 217);
    border: solid 5px rgb(223, 188, 11);
  }
  .blocks {
    display: flex;
  }
  .block {
    height: 5rem;
    border-radius: 0.2rem;
    width: 1rem;
  }
  .block.red {
    background-color: red;
  }
  .block.green {
    background-color: green;
  }
  .block.yellow {
    background-color: rgb(223, 188, 11);
  }
  .block.blue {
    background-color: blue;
  }
</style>
