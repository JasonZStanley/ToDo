<script lang="ts">
    import { onMount } from 'svelte'
    import { supabase } from '../supabaseClient'
    import type { AuthSession } from '@supabase/supabase-js'
    import { PUBLIC_URL } from '$env/static/public';
    import { goto } from '$app/navigation';
  
    let session: AuthSession | null
  
    onMount(() => {
      supabase.auth.getSession().then(({ data }) => {
        session = data.session
      })
  
      supabase.auth.onAuthStateChange((_event, _session) => {
        session = _session

        if (_event === 'PASSWORD_RECOVERY') {
            throw goto(PUBLIC_URL + 'account/security')
        }

        console.log(_event, session)
      })
    })
  </script>
  
  <div class="container" style="padding: 50px 0 100px 0">
    {#if !session}
        <p>Guest</p>
        <slot />
    {:else}
        <p>Authenticated</p>
        <slot />
    {/if}
  </div>