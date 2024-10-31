<script lang="ts">
  import type { Product } from '$lib/types';

  export let products: Product[] = [];
</script>

<div
  class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4"
>
  {#each products as product}
    <div class="border p-4 rounded-md shadow-md">
      <h2 class="text-lg font-bold">{product.name}</h2>
      <p class="text-gray-500">${product.price}</p>
    </div>
  {/each}
</div>
