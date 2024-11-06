<script lang="ts">
  import { dark_mode } from "$lib/color";
  import type { Product } from "$lib/types";

  const handleProductClick = (id: string) => {
    console.log(id);
  };

  export let products: Product[] = [];
</script>

<div
  class="px-4 sm:px-10 pb-10 pt-5 rounded-lg"
  style={`background-color: ${dark_mode['background-secondary']}`}
>
  <div class="pb-3 flex flex-col sm:flex-row items-center justify-between gap-4 sm:gap-0">
    <h1 class="text-[32px] sm:text-[40px] font-bold">Products</h1>

    <!-- Search input -->
    <div class="relative w-full sm:w-auto">
      <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
        <svg class="h-5 w-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
        </svg>
      </div>
      <input 
        type="text" 
        placeholder="Search" 
        class="w-full h-[30] text-white rounded-md p-2 pl-10 outline-none" 
        style={`background-color: ${dark_mode['background-primary']}`} 
        aria-label="Search"
      />
    </div>
  </div>
  <div
    class="grid grid-cols-1 xs:grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-4"
  >
    {#each products as product}
      <button
        onmouseenter={(e) => {
          const img = e.currentTarget.querySelector("img");
          if (img) {
            img.style.transform = "scale(1.12)";
            img.style.transition = "transform 0.2s";
          }
        }}
        onmouseleave={(e) => {
          const img = e.currentTarget.querySelector("img");
          if (img) {
            img.style.transform = "scale(1)";
          }
        }}
        onclick={() => handleProductClick(product.id)}
      >
        <div
          class="border p-4 rounded-md shadow-md flex flex-col items-center shadow-gray-500"
        >
          <img src={product.logo} alt={product.name} class="w-[130px] h-auto" />
          <p class="pt-3 text-center">{product.name}</p>
        </div>
      </button>
    {/each}
  </div>
</div>
