<script lang="ts">
    import { supabase } from "../../../supabaseClient";
  
    let email: string
    let password: string
    let serverError = '';
    let success = false;

    const register = async () => {
      serverError = ''

      try {
        const { data, error } = await supabase.auth.signUp({ email, password });

        if (error) {
          serverError = error.message
        } else {
          if (data.user?.identities && data.user.identities.length) {
            success = true
          } else {
            serverError = "Account Registered. Please login."
          }
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
      <p class="success">An email has been sent to the address specified. Please click on the confirmation link to finish registration</p>
    {:else}
    <form action="#" method="POST" on:submit|preventDefault={register} class="form-widget">
      <div>
        <label for="email">Email</label>
        <input id="email" type="text" bind:value={email} />
      </div>
      <div>
        <label for="password">Password</label>
        <input id="password" type="password" bind:value={password} />
      </div>
      <input type="submit" value="Register" />
    </form>
    {/if}