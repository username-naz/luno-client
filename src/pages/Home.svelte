<script lang="ts">
  import { navigate } from "svelte-routing";
  import { socket as socketS, data } from "../stores/session";
  import { Socket, io } from "socket.io-client";

  export let socket: Socket;
  let ip;
  let name;

  const handleConnect = () => {
    try {
      socket = io(ip);
    } catch (e) {
      console.log(e);
    }
    socket.on("connect", () => {
      socketS.set(socket);
    });

    socket.on("environment-update", (res) => {
      data.set(res.data);
      console.log(res.data);
    });
  };
</script>

<div>
  <label for="server">Enter Server IP</label>
  <input
    name="ser
  ver"
    bind:value={ip}
  />
  <button on:click={handleConnect}>Connect</button>
</div>

{#if $data}
  <h4 style="color:green;">
    Connected to Server. Server Status: {$data.environment.status}
  </h4>
  {#if $data.environment.host}
    <h4>Server Host: {$data.environment.host.name}</h4>
  {/if}
{/if}
<br />
<div>
  <label for="name">Name</label>
  <input name="name" bind:value={name} />
  <button
    on:click={() => {
      socket.emit("register-player", { name });
    }}>Register</button
  >
</div>

<button
  on:click={() => {
    socket.emit("create-game");
    setTimeout(() => {
      navigate("/game");
    }, 1000);
  }}>Start Game</button
>
{#if $data}
  <div>
    <h3>Players Connected</h3>
    {#each $data.connections as connection, index}
      <div>{index + 1}. {connection.name}</div>
    {/each}
  </div>
{/if}
