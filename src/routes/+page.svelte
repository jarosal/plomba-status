<script lang="ts">
  import { backOut } from "svelte/easing";
  import { fly } from "svelte/transition";
  import { onMount } from "svelte";
  import { PUBLIC_PLOMBA_PRICE } from '$env/static/public'

  const price = +PUBLIC_PLOMBA_PRICE;
  let show = false;

  onMount(() => (show = true));

  $: isProfitable = price <= 25;

  let decision: string = isProfitable ? "TAK" : "NIE";

  const words = ["Czy opłaca sie", "", "zerwać plombe", "", "na funfit?"];
</script>

<div class="flex flex-col place-content-center min-h-screen">
  <div
    class="flex flex-col items-center justify-items-center text-5xl m-2 p-2 gap-2"
  >
    <div class="flex flex-col card m-4 p-4 pb-6">
      <div class="inline-block overflow-hidden max-w-[900px] text-center">
        {#each words as word, i}
          {#if show}
            <span
              in:fly={{
                y: 100,
                delay: 300 * i,
                easing: backOut,
              }}
              class="inline-block m-1"
            >
              {word}
            </span>
          {/if}
        {/each}
      </div>
      {#if show}
        <div class="m-2 pt-4 text-center tracking-wide">
          <p
            in:fly={{
              y: 100,
              delay: 300 * (words.length + 1),
              easing: backOut,
            }}
            class="font-bold"
            class:text-success-500={isProfitable}
            class:text-error-500={!isProfitable}
          >
            {decision}
          </p>
        </div>
      {/if}
      {#if show}
        <div class="inline-block text-center">
          <p
            in:fly={{
              y: 50,
              delay: 300 * (words.length + 2),
              easing: backOut,
            }}
            class="text-strong"
          >
            Aktualna cena to {price} zł
          </p>
        </div>
      {/if}
    </div>
  </div>
</div>
