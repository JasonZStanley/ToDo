<script lang="ts">
    import { supabase } from "../../../supabaseClient";
  
    let email: string
    let password: string
    let serverError = '';
    let success = false;

    const login = async () => {
      serverError = ''

      try {
        const { data, error } = await supabase.auth.signInWithPassword({ email, password });

        if (error) {
          serverError = error.message
        } else {
          success = true
        }

      } catch (e) {
        serverError = "Something unexpected happened. Please wait a moment and try again."
      }
    }
  </script>


    {#if serverError}
      <p class="error">{serverError}</p>
    {/if}

    {#if success}
      <p class="success">Welcome!</p>
    {:else}
    <form action="#" method="POST" on:submit|preventDefault={login} class="form-widget">
      <div>
        <label for="email">Email</label>
        <input id="email" type="text" bind:value={email} />
      </div>
      <div>
        <label for="password">Password</label>
        <input id="password" type="password" bind:value={password} />
      </div>
      <input type="submit" value="Login" />
    </form>
    {/if}