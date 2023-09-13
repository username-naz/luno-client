<script lang="ts">
  export let cardStack;
</script>

{#if cardStack.color}
  <h3>
    Color: <span style="color: {cardStack.color};"
      >{cardStack.color.toUpperCase()}</span
    >
  </h3>
{/if}

<div class="container">
  {#if !cardStack.stack.length}
    <div class="card hollow" />
  {/if}
  {#each cardStack.stack as card}
    <div class="card {card.type} {card.color} {card.subType}">
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
    margin-left: -6rem;
    width: 3rem;
    height: 7.5rem;
    border-radius: 0.5rem;
    position: relative;
    background-color: white;
  }

  .card.hollow {
    background: none;
    border: 1px grey solid;
  }
  .center {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-weight: 600;
    font-size: 4rem;
    aspect-ratio: 1;
    border-radius: 50%;
    background: white;
    padding: 0.5rem;
  }

  .draw_two .center {
    font-size: 3rem;
  }

  .topLeft {
    position: absolute;
    top: 0.5rem;
    left: 0.5rem;
    transform: translate(-50%, -50%);
    font-weight: 600;
    font-size: 1rem;
    aspect-ratio: 1;
    border-radius: 50%;
    width: 0;
    height: 0;
  }
  .bottomRight {
    position: absolute;
    bottom: 1.5rem;
    right: 0rem;
    transform: translate(-50%, -50%);
    font-weight: 600;
    font-size: 1rem;
    aspect-ratio: 1;
    border-radius: 50%;
    height: 0;
  }

  .wild {
    border: solid 2px white;
    background-color: black;
  }
  .red {
    color: red;
    background-color: rgb(239, 217, 217);
    border: solid 2px red;
  }
  .blue {
    color: blue;
    background-color: rgb(217, 219, 239);
    border: solid 2px blue;
  }
  .green {
    color: green;
    background-color: rgb(217, 239, 217);
    border: solid 2px green;
  }
  .yellow {
    color: rgb(199, 199, 14);
    background-color: rgb(239, 235, 217);
    border: solid 2px rgb(223, 188, 11);
  }
  .blocks {
    display: flex;
  }
  .block {
    height: 2.5rem;
    border-radius: 0.1rem;
    width: 0.5rem;
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
