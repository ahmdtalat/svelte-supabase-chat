<script lang="ts">
  import { store } from './store'
  import Chat from './lib/Chat.svelte'
  import Login from './lib/Login.svelte'
</script>

<main>
  <h2>Svelte & Supabase Chat</h2>
  {#if $store.user}
    <Chat />
  {:else}
    <Login />
  {/if}
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans',
      'Helvetica Neue', sans-serif;
    background-color: rgb(39, 36, 36);
  }

  h2 {
    color: #0088ff;
  }

  main {
    text-align: center;
    padding: 1em;
  }
</style>
