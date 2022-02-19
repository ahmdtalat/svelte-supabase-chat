<script>
  import { fade } from 'svelte/transition'
  import { onMount, beforeUpdate, afterUpdate } from 'svelte'

  import db, { store } from '../store'
  import Message from './Message.svelte'

  let loading = false

  // handle auto scroll
  let div
  let autoscroll

  beforeUpdate(() => {
    autoscroll = div && div.offsetHeight + div.scrollTop > div.scrollHeight - 20
  })

  afterUpdate(() => {
    if (autoscroll) div.scrollTo(0, div.scrollHeight)
  })

  onMount(async () => {
    loading = true
    const res = await db.msg.getAll()
    store.update((oldStore) => ({
      ...oldStore,
      msgs: res
    }))
    loading = false
  })
</script>

<div class="messages" bind:this={div} in:fade>
  {#if $store.msgs.length}
    {#each $store.msgs as msg (msg.id)}
      <Message {msg} />
    {/each}
  {:else if loading}
    <p class="loading">Loading...</p>
  {:else}
    <p class="empty">No msgs</p>
  {/if}
</div>

<style>
  .messages {
    flex: 1;
    overflow-x: hidden;
    overflow-y: auto;
    margin-top: 4px;
  }
  .empty,
  .loading {
    font-size: 16px;
    letter-spacing: 1px;
    color: gray;
  }
</style>
