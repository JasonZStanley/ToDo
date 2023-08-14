<script lang="ts">
    import { supabase } from "../../../supabaseClient";
  
    let password: string
    let serverError = '';
    let success = false;

    const register = async () => {
      serverError = ''

      try {
        const { data, error } = await supabase.auth.updateUser({ password })

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
      <p class="success">Your password has been updated.</p>
    {:else}
    <form action="#" method="POST" on:submit|preventDefault={register} class="form-widget">
      <div>
        <label for="password">Password</label>
        <input id="password" type="password" bind:value={password} />
      </div>
      <input type="submit" value="Update Password" />
    </form>
    {/if}