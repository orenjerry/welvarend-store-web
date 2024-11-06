<script lang="ts">
  import { products, news } from "$lib/data";
  import ProductGrid from "../components/ProductGrid.svelte";
  import NewsCarousel from "../components/NewsCarousel.svelte";
</script>

<svelte:head>
  <title>Beranda | Welvarend Store</title>
</svelte:head>

<section>
  <!-- News section -->
  <div class="relative mx-auto mt-10 px-4 sm:px-0 max-w-[900px] w-full">
      <NewsCarousel {news} />
  </div>
  <!-- end of news section -->

  <!-- Products section -->
  <div class="container mx-auto p-4 text-white">
      <ProductGrid {products} />
  </div>
  <!-- end of products section -->
</section>
