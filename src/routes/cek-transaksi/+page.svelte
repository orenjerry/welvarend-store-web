<script>
    import { dark_mode } from "$lib/color";
    let invoice = $state("");
    let inputValue = $state("");
    let isLoading = $state(false);
</script>

<svelte:head>
    <title>Cek Transaksi | Welvarend Store</title>
</svelte:head>

<section>
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-white">
        <h1 class="text-3xl font-bold text-center mt-10">
            Cari Transaksi Kamu!
        </h1>
        <p class="text-center pt-2">
            Lacak transaksi kamu dengan cara memasukkan Nomor Invoice di bawah
            ini:
        </p>
        <!-- Search input -->
        <div class="flex w-full sm:w-[500px] mx-auto mt-3 gap-2">
            <div class="relative flex-1">
                <div
                    class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none"
                >
                    <svg
                        class="h-5 w-5 text-gray-400"
                        fill="none"
                        stroke="currentColor"
                        viewBox="0 0 24 24"
                    >
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
                        />
                    </svg>
                </div>
                <input
                    bind:value={inputValue}
                    type="text"
                    placeholder="Search"
                    class="w-full h-10 text-white rounded-md p-2 pl-10 outline-none [&::placeholder]:normal-case uppercase"
                    style={`background-color: ${dark_mode["background-primary"]}`}
                    aria-label="Search"
                    onkeydown={(e) => {
                        if (e.key === 'Enter') {
                            isLoading = true;
                            invoice = inputValue.toUpperCase();
                            setTimeout(() => {
                                isLoading = false;
                            }, 1000);
                        }
                    }}
                />
            </div>
            <button 
                class="h-10 px-4 rounded-md bg-blue-600 hover:bg-blue-700"
                onclick={() => {
                    isLoading = true;
                    invoice = inputValue.toUpperCase();
                    setTimeout(() => {
                        isLoading = false;
                    }, 1000);
                }}
            >
                Cari
            </button>
        </div>
        {#if invoice}
            <div
                class="mt-3 w-full rounded-md p-4"
                style={`background-color: ${dark_mode["background-secondary"]}`}
            >
                {#if isLoading}
                    <div class="flex justify-center items-center">
                        <div class="animate-spin rounded-full h-8 w-8 border-b-2 border-white"></div>
                    </div>
                {:else}
                    <h1 class="text-2xl font-bold text-center">Invoice : #{invoice}</h1>

                {/if}
            </div>
        {/if}
    </div>
</section>
