<script lang="ts">
  import db, { store } from '../store'
  import MsgForm from './MsgForm.svelte'
  import Messages from './Messages.svelte'
</script>

<svelte:head>
  <title>Svelte Chat App</title>
</svelte:head>

<div class="chat">
  <section>
    <strong>{$store.user.email} ❤‍🔥</strong>
    <button on:click={db.logout}>Logout</button>
  </section>

  <!-- Messgaes -->
  <Messages />
  <MsgForm />
</div>

<style>
  .chat {
    display: flex;
    flex-direction: column;
    margin: auto;
    max-width: 600px;
    box-shadow: 1px 1px 5px 0px rgba(0, 0, 0, 0.55);
    height: 80vh;
    border-radius: 8px;
    overflow: hidden;
  }
  section {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 55px;
    background-color: #0088ff;
    padding: 0 1rem;
    border-top-right-radius: 8px;
    border-top-left-radius: 8px;
  }
  section button {
    height: 35px;
    width: 100px;
    border-radius: 5px;
    border: none;
    box-shadow: 1px 1px 5px 0px rgba(0, 0, 0, 0.35);
    cursor: pointer;
    font-weight: bold;
  }
  section button:active {
    background-color: gray;
  }
</style>
