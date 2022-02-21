<script>
  import { replace } from 'svelte-spa-router'

  import db from '../store'

  let email = ''
  let loading = false

  const handleLogin = async () => {
    if (!email.trim()) return

    loading = true
    await db.login({
      email
    })
    loading = false
    replace('/')
  }
</script>

<svelte:head>
  <title>Svelte Chat App | Login</title>
</svelte:head>

<form on:submit|preventDefault={handleLogin}>
  <h3>Login</h3>
  <input type="email" bind:value={email} placeholder="Email" />
  <button type="submit">{loading ? 'Login...' : 'Login'}</button>
</form>

<style>
  h3 {
    color: gray;
  }
  form {
    display: flex;
    flex-direction: column;
    justify-content: center;
    background-color: rgb(39, 36, 36);

    padding: 1rem;
    max-width: 400px;
    margin: auto;
    border-radius: 10px;
    height: 200px;
    box-shadow: 1px 1px 5px 0px rgba(0, 0, 0, 0.5);
  }
  input {
    margin: 0.2rem;
    height: 50px;
    padding: 0 1rem;
    border-radius: 8px;
    border: 0.4px solid gray;
    background-color: rgb(39, 36, 36);

    box-shadow: 1px 1px 5px 0px rgba(0, 0, 0, 0.15);
    color: #ccc;
    font-size: 16px;
    font-weight: 500;
  }

  button {
    background-color: #0088ff;
    color: white;
    font-weight: bold;
    letter-spacing: 3px;
    padding: 14px 20px;
    margin: 8px 0;
    border: none;
    cursor: pointer;
    width: 100%;
    border-radius: 8px;
    transition: all 0.5s cubic-bezier(0.075, 0.82, 0.165, 1);
  }
  button:active {
    background: blue;
  }
</style>
