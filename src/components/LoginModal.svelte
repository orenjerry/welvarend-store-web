<script lang="ts">
    import { dark_mode } from "$lib/color";
    import { fade, scale } from "svelte/transition";
    let username = $state("");
    let password = $state("");
    let isLoading = $state(false);
    let { showModal, setShowModal } = $props<{
        showModal: boolean;
        setShowModal: (value: boolean) => void;
    }>();

    function handleSubmit() {
        isLoading = true;
        // Add login logic here
        setTimeout(() => {
            isLoading = false;
            setShowModal(false);
        }, 1000);
    }
</script>

{#if showModal}
    <div
        class="fixed inset-0 z-50 flex items-center justify-center"
        transition:fade={{ duration: 200 }}
    >
        <!-- Backdrop -->
        <button
            class="absolute inset-0 bg-black opacity-50"
            onclick={() => setShowModal(false)}
            transition:fade={{ duration: 200 }}
            aria-label="Close"
        ></button>

        <!-- Modal -->
        <div
            class="relative w-full max-w-md p-6 rounded-lg shadow-xl"
            style={`background-color: ${dark_mode["background-secondary"]}`}
            transition:scale={{ duration: 200, start: 0.95 }}
        >
            <div class="flex justify-between items-center mb-4">
                <h2 class="w-full text-xl font-bold text-white text-center justify-center">Login</h2>
            </div>

            <form onsubmit={handleSubmit} class="space-y-4">
                <div>
                    <label
                        for="username"
                        class="block text-sm font-medium text-white"
                        >Username</label
                    >
                    <input
                        id="username"
                        type="text"
                        bind:value={username}
                        class="mt-1 block w-full rounded-md text-white p-2 outline-none"
                        style={`background-color: ${dark_mode["background-primary"]}`}
                        required
                    />
                </div>

                <div>
                    <label
                        for="password"
                        class="block text-sm font-medium text-white"
                        >Password</label
                    >
                    <input
                        id="password"
                        type="password"
                        bind:value={password}
                        class="mt-1 block w-full rounded-md text-white p-2 outline-none"
                        style={`background-color: ${dark_mode["background-primary"]}`}
                        required
                    />
                </div>

                <button
                    type="submit"
                    class="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-blue-600 hover:bg-blue-700 focus:outline-none"
                    disabled={isLoading}
                >
                    {#if isLoading}
                        <div
                            class="animate-spin rounded-full h-5 w-5 border-b-2 border-white"
                        ></div>
                    {:else}
                        Login
                    {/if}
                </button>
            </form>
            <hr class="mt-5">

            <div class="mt-4 text-sm text-center">
                <a
                    href="/auth/register"
                    class="text-blue-400 hover:text-blue-300"
                >
                    Don't have an account? Register here
                </a>
            </div>
        </div>
    </div>
{/if}
