<script lang="ts">
    import { supabase } from "../../../supabaseClient";
    import { onMount } from "svelte";
    import { PUBLIC_URL } from "$env/static/public";
    import { goto } from "$app/navigation";

    onMount(() => {
        const { error } = supabase.auth.signOut().then(() => {
            throw goto(PUBLIC_URL + 'account/login')
        })
    });
</script>