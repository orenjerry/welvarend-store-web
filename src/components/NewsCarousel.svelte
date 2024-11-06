<script lang="ts">
  import { onMount } from "svelte";
  import type { NewsBanner } from "$lib/types";
  onMount(() => {
    const glide = new Glide(".glide", { // ignore this error
      type: "carousel",
      autoplay: news.length > 1 ? 3800 : false,
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

  export let news: NewsBanner[] = [];
</script>

<svelte:head>
  <script src="node_modules/@glidejs/glide/dist/glide.min.js"></script>
  <link
    rel="stylesheet"
    href="../node_modules/@glidejs/glide/dist/css/glide.core.min.css"
  />
  <link
    rel="stylesheet"
    href="../node_modules/@glidejs/glide/dist/css/glide.theme.min.css"
  />
</svelte:head>

<div class="glide rounded-2xl w-full">
  <div class="glide__track" data-glide-el="track">
    <ul class="glide__slides">
      {#each news as image}
        <li class="glide__slide">
          <img
            src={image.src}
            alt={image.alt}
            class="w-full h-[200px] sm:h-[300px] object-cover rounded-2xl"
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
