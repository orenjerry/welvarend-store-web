<script lang="ts">
  import { news as newsData } from "$lib/data";
  import Glide from "@glidejs/glide";
  import { onMount } from "svelte";
  import type { NewsBanner } from "$lib/types";
  onMount(() => {
    const glide = new Glide(".glide", {
      type: "carousel",
      autoplay: 3800,
      animationDuration: 500,
      gap: 0,
      perView: 1,
      hoverpause: true,
    });

    glide.mount();

    return () => {
      glide.destroy();
    };
  });

  export let news: NewsBanner[] = newsData;
</script>

<svelte:head>
  <link
    rel="stylesheet"
    href="https://cdn.jsdelivr.net/npm/@glidejs/glide/dist/css/glide.core.min.css"
  />
  <link
    rel="stylesheet"
    href="https://cdn.jsdelivr.net/npm/@glidejs/glide/dist/css/glide.theme.min.css"
  />
</svelte:head>

<div class="glide">
  <div class="glide__track" data-glide-el="track">
    <ul class="glide__slides">
      {#each news as image}
        <li class="glide__slide">
          <img
            src={image.src}
            alt={image.alt}
            class="w-full h-[300px] object-cover rounded-2xl"
          />
        </li>
      {/each}
    </ul>
  </div>

  <!-- Bullets -->
  <div class="flex items-center justify-center gap-4 mt-4">
    <div class="glide__bullets flex gap-2" data-glide-el="controls[nav]">
      {#each news as _, i}
        <button
          class="glide__bullet"
          data-glide-dir={`=${i}`}
          aria-label={`Go to slide ${i + 1}`}
        ></button>
      {/each}
    </div>
  </div>
</div>