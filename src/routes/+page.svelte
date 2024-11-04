<script lang="ts">
  import { products, news } from "$lib/data";
  import ProductGrid from "../components/ProductGrid.svelte";
  import NewsCarousel from "../components/NewsCarousel.svelte";
</script>

<section>
  <!-- News section -->
  <div class="relative max-w-6xl mx-auto mt-10 w-[900px]">
    <NewsCarousel {news} />
  </div>
  <!-- end of news section -->

  <!-- Products section -->
  <div class="container mx-auto p-4 text-white h-100">
    <h1 class="text-2xl font-bold">Products</h1>
    <ProductGrid {products} />
  </div>
  <!-- end of products section -->
</section>
