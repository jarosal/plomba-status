<script lang="ts">
    import { fly } from "svelte/transition"

    let price: number = 50;
    $: isProfitable = price <= 25

    let words = ['Czy opłaca się', 'zerwać plombe', 'na funfit>']
</script>

<div class="flex flex-col place-content-center min-h-screen">
    <div class="flex flex-col items-center justify-items-center text-5xl m-2 p-2 gap-2">
        <span class="gradient-heading">Czy opłaca się zerwać plombe na funfit? </span>
        <p></p>
        <p class:text-success-500={isProfitable} class:text-error-500={!isProfitable}>{isProfitable ? "TAK" : "NIE"}</p>
        <p>Aktualna cena to {price} zł</p>
    </div>
</div>

