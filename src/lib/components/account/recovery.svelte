<script lang="ts">
    import { supabase } from "../../../supabaseClient";
    import { PUBLIC_URL } from "$env/static/public";
  
    let email: string
    let serverError = '';
    let success = false;

    const login = async () => {
      serverError = ''

      try {
        const { data, error } = await supabase.auth.resetPasswordForEmail(email)

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
      <p class="success">Please check your email to change your password.</p>
    {:else}
    <form action="#" method="POST" on:submit|preventDefault={login} class="form-widget">
      <div>
        <label for="email">Email</label>
        <input id="email" type="text" bind:value={email} />
      </div>
      <input type="submit" value="Recover Password" />
    </form>
    {/if}