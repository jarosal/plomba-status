<script lang="ts">
  import { backOut } from "svelte/easing";
  import { fly } from "svelte/transition";
  import { onMount } from "svelte";
  import { PUBLIC_PLOMBA_PRICE } from '$env/static/public'

  const plombaPrice = +PUBLIC_PLOMBA_PRICE;
  const isPlombaWorthBreaking = plombaPrice <= 25;

  let verdict = isPlombaWorthBreaking ? "TAK" : "NIE";
  
  const words = ["Czy opłaca sie", "", "zerwać plombe", "", "na funfit?"];

  let showAnimations = false;
  onMount(() => (showAnimations = true));
</script>

<div class="flex flex-col place-content-center min-h-screen">
  <div
    class="flex flex-col items-center justify-items-center text-5xl m-2 p-2 gap-2"
  >
    <div class="flex flex-col card m-4 p-4 pb-6">
      <div class="inline-block overflow-hidden max-w-[900px] text-center">
        {#each words as word, i}
          {#if showAnimations}
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
      {#if showAnimations}
        <div class="m-2 pt-4 text-center tracking-wide">
          <p
            in:fly={{
              y: 100,
              delay: 300 * (words.length + 1),
              easing: backOut,
            }}
            class="font-bold"
            class:text-success-500={isPlombaWorthBreaking}
            class:text-error-500={!isPlombaWorthBreaking}
          >
            {verdict}
          </p>
        </div>
      {/if}
      {#if showAnimations}
        <div class="inline-block text-center">
          <p
            in:fly={{
              y: 50,
              delay: 300 * (words.length + 2),
              easing: backOut,
            }}
            class="text-strong"
          >
            Aktualna cena to {plombaPrice} zł
          </p>
        </div>
      {/if}
    </div>
  </div>
</div>
