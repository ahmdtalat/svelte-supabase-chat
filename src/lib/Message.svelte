<script>
  import { fly } from 'svelte/transition'
  import { store } from '../store'

  export let msg
</script>

<div in:fly={{ y: 20, duration: 200 }} class={`container ${msg.username === $store.user.email ? 'right' : 'left'}`}>
  {#if msg.username !== $store.user.email}
    <p>{msg.username.split('@')[0]}</p>
  {/if}
  <div>
    {msg.text}
  </div>
</div>

<style>
  .container {
    width: fit-content;
    margin: 1rem 0;
  }

  .right {
    margin-left: auto;
    margin-right: 1rem;
  }

  .left {
    margin-left: 1rem;
  }
  p {
    margin-bottom: 3px;
    font-weight: 600;
    text-align: right;
    color: rgb(83, 80, 80);
  }

  .left p {
    text-align: left;
    color: #0088ff;
  }

  .container > div {
    padding: 1rem;
    width: fit-content;
    max-width: 350px;
    border-radius: 8px;
    box-shadow: 1px 1px 5px 0px rgba(0, 0, 1, 1);
    text-align: left;
    word-break: break-all;
  }

  .right > div {
    background-color: #5744c5;
    color: #fff;
  }
  .left > div {
    color: blue;
    background-color: #fff;
  }

  @media screen and (max-width: 768px) {
    .container > div {
      max-width: 60vw;
    }
  }
</style>
