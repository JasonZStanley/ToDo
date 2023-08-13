<script lang="ts">
    import { supabase } from "../../../supabaseClient";
    import { onMount } from "svelte";

    onMount(() => {
        const { error } = supabase.auth.signOut().then(() => {})
    });
</script>