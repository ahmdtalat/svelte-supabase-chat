<script lang="ts">
  import { wrap } from 'svelte-spa-router/wrap'
  import Route, { replace, type ConditionsFailedEvent } from 'svelte-spa-router'

  import { supabase } from './store'
  import Logout from './lib/Logout.svelte'
  import NotFound from './lib/NotFound.svelte'

  function conditionsFailed(event: ConditionsFailedEvent) {
    if (event.detail.route === '/') replace('/login')
    else replace('/')
  }
</script>

<main>
  <h2>Svelte & Supabase Chat</h2>
  <Route
    routes={{
      '/': wrap({
        asyncComponent: () => import('./lib/Chat.svelte'),
        conditions: [
          () => {
            return Boolean(supabase.auth.user())
          }
        ]
      }),
      '/login': wrap({
        asyncComponent: () => import('./lib/Login.svelte'),
        conditions: [
          () => {
            return !supabase.auth.user()
          }
        ]
      }),
      '/logout': Logout,
      '*': NotFound
    }}
    on:conditionsFailed={conditionsFailed}
  />
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
