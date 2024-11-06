<script lang="ts">
	import '../app.css';
	import { dark_mode } from '$lib/color';
	import { onMount } from 'svelte';

	let { children } = $props();
	let scrollY = $state(0);
	let isMenuOpen = $state(false);

	onMount(() => {
		const handleScroll = () => {
			scrollY = window.scrollY;
		};
		window.addEventListener('scroll', handleScroll);
		return () => {
			window.removeEventListener('scroll', handleScroll);
		};
	});
</script>

<main class="min-h-screen w-full" style={`background-color: ${dark_mode['background-primary']}`}>
	<!-- Navbar -->
	<nav class="sticky top-0 w-full transition-all duration-200 z-10" style={`background-color: ${dark_mode['background-secondary']}`}>
		<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
			<div class="flex justify-between h-16">
				<div class="flex">
					<!-- Logo -->
					<div class="flex-shrink-0 flex items-center">
						<a href="/">
							<img src="/images/Logo.png" alt="Welvarend Store" class="h-[50px] sm:hidden w-auto" />
							<img src="/images/LogoL.png" alt="Welvarend Store" class="hidden sm:block sm:h-[100px] w-auto" />
						</a>
					</div>

					<div class="hidden sm:ml-6 sm:flex sm:space-x-8">
						<a
							href="#"
							class="inline-flex items-center px-1 text-sm font-medium"
						>
							Beranda
						</a>
						<a
							href="#"
							class="inline-flex items-center px-1 text-sm font-medium"
						>
							Posts
						</a>
						<a
							href="#"
							class="inline-flex items-center px-1 text-sm font-medium"
						>
							Cek Transaksi
						</a>
					</div>
				</div>

				<div class="flex items-center gap-2">
					<a
						href="#"
						class="p-2 text-gray-400 hover:text-gray-500 transition-colors duration-200"
						aria-label="Account"
					>
						<svg
							class="h-6 w-6"
							fill="none"
							stroke="currentColor"
							viewBox="0 0 24 24"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
							/>
						</svg>
					</a>

					<div class="sm:hidden flex items-center">
						<button
							type="button"
							class="text-gray-400 hover:text-gray-500 transition-colors duration-200"
							on:click={() => isMenuOpen = !isMenuOpen}
						>
							<svg class="h-6 w-6 transition-transform duration-200" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									class={`transform transition-opacity duration-200 ${isMenuOpen ? "opacity-0" : "opacity-100"}`}
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M4 6h16M4 12h16M4 18h16"
								/>
								<path
									class={`transform transition-opacity duration-200 absolute ${!isMenuOpen ? "opacity-0" : "opacity-100"}`}
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M6 18L18 6M6 6l12 12"
								/>
							</svg>
						</button>
					</div>
				</div>
			</div>

			<!-- Mobile menu -->
			{#if isMenuOpen}
				<div 
					class="sm:hidden fixed inset-x-0 top-16 z-50 transition-all duration-300 ease-in-out"
					style={`background-color: ${dark_mode['background-secondary']}`}
				>
					<div class="pt-2 pb-3 space-y-1">
						<a
							href="#"
							class="block px-3 py-2 text-base font-medium transition-all duration-300 hover:text-gray-300"
							style="
								transform: translateX({isMenuOpen ? '0' : '-100%'});
								opacity: {isMenuOpen ? '1' : '0'};
								transition-delay: 100ms;
							"
						>
							Beranda
						</a>
						<a
							href="#"
							class="block px-3 py-2 text-base font-medium transition-all duration-300 hover:text-gray-300"
							style="
								transform: translateX({isMenuOpen ? '0' : '-100%'});
								opacity: {isMenuOpen ? '1' : '0'};
								transition-delay: 150ms;
							"
						>
							Posts
						</a>
						<a
							href="#"
							class="block px-3 py-2 text-base font-medium transition-all duration-300 hover:text-gray-300"
							style="
								transform: translateX({isMenuOpen ? '0' : '-100%'});
								opacity: {isMenuOpen ? '1' : '0'};
								transition-delay: 200ms;
							"
						>
							Cek Transaksi
						</a>
					</div>
				</div>
			{/if}
		</div>
	</nav>
	<!-- end of navbar -->

	<!-- Children -->
	{@render children()}
	<!-- end of children -->

	<!-- Footer -->
	<footer class="text-white mt-auto w-full" style={`background-color: ${dark_mode['background-secondary']}`}>
		<div class="container mx-auto p-4">
			<div class="flex flex-col lg:flex-row gap-8">
				<div class="flex flex-col items-center lg:items-start">
					<img 
						src="/images/LogoL.png" 
						alt="Welvarend Store Logo" 
						class="h-[150px] lg:h-[200px] w-auto lg:pr-5" 
					/>
					<div class="flex gap-4 mt-2">
						<a href="#">
							<svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
								<path d="M12.315 2c2.43 0 2.784.013 3.808.06 1.064.049 1.791.218 2.427.465a4.902 4.902 0 011.772 1.153 4.902 4.902 0 011.153 1.772c.247.636.416 1.363.465 2.427.048 1.067.06 1.407.06 4.123v.08c0 2.643-.012 2.987-.06 4.043-.049 1.064-.218 1.791-.465 2.427a4.902 4.902 0 01-1.153 1.772 4.902 4.902 0 01-1.772 1.153c-.636.247-1.363.416-2.427.465-1.067.048-1.407.06-4.123.06h-.08c-2.643 0-2.987-.012-4.043-.06-1.064-.049-1.791-.218-2.427-.465a4.902 4.902 0 01-1.772-1.153 4.902 4.902 0 01-1.153-1.772c-.247-.636-.416-1.363-.465-2.427-.047-1.024-.06-1.379-.06-3.808v-.63c0-2.43.013-2.784.06-3.808.049-1.064.218-1.791.465-2.427a4.902 4.902 0 011.153-1.772A4.902 4.902 0 015.45 2.525c.636-.247 1.363-.416 2.427-.465C8.901 2.013 9.256 2 11.685 2h.63zm-.081 1.802h-.468c-2.456 0-2.784.011-3.807.058-.975.045-1.504.207-1.857.344-.467.182-.8.398-1.15.748-.35.35-.566.683-.748 1.15-.137.353-.3.882-.344 1.857-.047 1.023-.058 1.351-.058 3.807v.468c0 2.456.011 2.784.058 3.807.045.975.207 1.504.344 1.857.182.466.399.8.748 1.15.35.35.683.566 1.15.748.353.137.882.3 1.857.344 1.054.048 1.37.058 4.041.058h.08c2.597 0 2.917-.01 3.96-.058.976-.045 1.505-.207 1.858-.344.466-.182.8-.398 1.15-.748.35-.35.566-.683.748-1.15.137-.353.3-.882.344-1.857.048-1.055.058-1.37.058-4.041v-.08c0-2.597-.01-2.917-.058-3.96-.045-.976-.207-1.505-.344-1.858a3.097 3.097 0 00-.748-1.15 3.098 3.098 0 00-1.15-.748c-.353-.137-.882-.3-1.857-.344-1.023-.047-1.351-.058-3.807-.058zM12 6.865a5.135 5.135 0 110 10.27 5.135 5.135 0 010-10.27zm0 1.802a3.333 3.333 0 100 6.666 3.333 3.333 0 000-6.666zm5.338-3.205a1.2 1.2 0 110 2.4 1.2 1.2 0 010-2.4z"/>
							</svg>
						</a>
						<a href="#">
							<svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24">
								<path d="M20.317 4.37a19.791 19.791 0 00-4.885-1.515.074.074 0 00-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 00-5.487 0 12.64 12.64 0 00-.617-1.25.077.077 0 00-.079-.037A19.736 19.736 0 003.677 4.37a.07.07 0 00-.032.027C.533 9.046-.32 13.58.099 18.057a.082.082 0 00.031.057 19.9 19.9 0 005.993 3.03.078.078 0 00.084-.028c.462-.63.874-1.295 1.226-1.994a.076.076 0 00-.041-.106 13.107 13.107 0 01-1.872-.892.077.077 0 01-.008-.128 10.2 10.2 0 00.372-.292.074.074 0 01.077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 01.078.01c.12.098.246.198.373.292a.077.077 0 01-.006.127 12.299 12.299 0 01-1.873.892.077.077 0 00-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 00.084.028 19.839 19.839 0 006.002-3.03.077.077 0 00.032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 00-.031-.03zM8.02 15.33c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.956-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.956 2.418-2.157 2.418zm7.975 0c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.955-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.946 2.418-2.157 2.418z"/>
							</svg>
						</a>
					</div>
				</div>

				<!-- Grid links -->
				<div class="grid grid-cols-2 sm:grid-cols-4 gap-8 lg:gap-[110px] pt-5 lg:pt-10">
					<div>
						<h3 class="font-bold mb-2">Services</h3>
						<ul class="space-y-1 text-sm">
							<li><a href="#">Help</a></li>
							<li><a href="#">Tools</a></li>
							<li><a href="#">Pricing</a></li>
						</ul>
					</div>
					<div>
						<h3 class="font-bold mb-2">Company</h3>
						<ul class="space-y-1 text-sm">
							<li><a href="#">About</a></li>
							<li><a href="#">Account</a></li>
							<li><a href="#">FAQ</a></li>
						</ul>
					</div>
					<div>
						<h3 class="font-bold mb-2">Helpful Links</h3>
						<ul class="space-y-1 text-sm">
							<li><a href="#">Contact</a></li>
							<li><a href="#">Support</a></li>
							<li><a href="#">FAQ</a></li>
						</ul>
					</div>
					<div>
						<h3 class="font-bold mb-2">Legal</h3>
						<ul class="space-y-1 text-sm">
							<li><a href="#">Accessibility</a></li>
							<li><a href="#">Returns Policy</a></li>
							<li><a href="#">Privacy Notice</a></li>
						</ul>
					</div>
				</div>
			</div>

			<div class="mt-8 text-sm text-center" style={`color: ${dark_mode['text-muted']}`}>
				<p>&copy; 2024 Welvarend Store. All rights reserved.</p>
			</div>
		</div>
	</footer>
	<!-- end of footer -->
</main>
