<script>
  import { onMount } from 'svelte'
  import { replace } from 'svelte-spa-router'

  import db from '../store'

  onMount(() => {
    db.logout()
    replace('/login')
  })
</script>
