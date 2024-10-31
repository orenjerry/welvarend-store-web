<script lang="ts">
  import { products } from "$lib/data";
  import ProductGrid from '../components/ProductGrid.svelte';
</script>

<svelte:head>
  <title>Welvarend Store</title>
  <meta name="description" content="Welcome to Welvarend Store" />
</svelte:head>

<section class="container mx-auto p-4 text-white h-screen">
  <h1 class="text-2xl font-bold">Products</h1>
  <ProductGrid {products}/>
</section>