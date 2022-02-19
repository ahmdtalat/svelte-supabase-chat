<script>
  import { onMount } from 'svelte'

  import db, { store, supabase } from '../store'

  let msg = ''
  let loading = false

  let input

  const handleSendMsg = async () => {
    if (msg.trim() === '') return
    loading = true
    await db.msg.send({
      username: $store.user.email,
      text: msg
    })
    msg = ''
    loading = false
  }

  onMount(() => {
    input.focus()

    const messages = supabase
      .from('messages')
      .on('*', (payload) => {
        store.update((old) => ({
          ...old,
          msgs: [...old.msgs, payload.new]
        }))
      })
      .subscribe()

    return () => messages.unsubscribe()
  })
</script>

<form on:submit|preventDefault={handleSendMsg}>
  <input bind:value={msg} placeholder="Enter a new msg" bind:this={input} />
  <button type="submit" disabled={loading}>{loading ? 'Sending...' : 'Send'}</button>
</form>

<style>
  form {
    height: 40px;
    width: 100%;
    display: flex;
    align-items: center;
    padding: 0.5rem 0;
    overflow: hidden;
    background-color: transparent;
  }
  form input {
    flex: 1;
    margin-right: 1rem;
    height: 100%;
    margin-left: 0.5rem;
    border: none;
    border-radius: 4px;
    padding: 0 1rem;
    font-weight: 500;
    font-size: 14px;

    border: 0.4px solid gray;
    box-shadow: 1px 1px 5px 0px rgba(0, 0, 0, 0.15);
    color: rgb(59, 75, 75);
    font-size: 16px;
    font-weight: 500;
  }

  button {
    height: 100%;
    width: 100px;
    padding: 14px 20px;
    margin-right: 0.5rem;
    background-color: #5744c5;
    color: white;
    font-weight: bold;
    letter-spacing: 1px;
    border: none;
    cursor: pointer;
    border-radius: 8px;
    transition: all 0.5s cubic-bezier(0.075, 0.82, 0.165, 1);
  }
  button:active {
    background: blue;
  }
</style>
