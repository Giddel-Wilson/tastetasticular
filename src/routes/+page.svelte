<script lang="ts">
	import { fade, fly, slide, scale } from 'svelte/transition';
	import { elasticOut } from 'svelte/easing';
	import { Search, Star, ChevronRight, Facebook, Twitter, Instagram } from 'lucide-svelte';
	import { Button } from '$lib/components/ui/button';
	import { Input } from '$lib/components/ui/input';
	import { Card } from '$lib/components/ui/card';
	import { Avatar } from '$lib/components/ui/avatar';
	import { Badge } from '$lib/components/ui/badge';
	import { onMount } from 'svelte';
	import chuck from '$lib/assets/chuck.png';
	import chef from '$lib/assets/chef.png';

	let mounted = false;
	let showSearch = false;
	let searchQuery = '';

	onMount(() => {
		console.log('Component mounted');
		mounted = true;
	});

	const categories = [
		{ name: 'Main Dish', icon: '🍽️' },
		{ name: 'Break Fast', icon: '🍳' },
		{ name: 'Dessert', icon: '🍰' },
		{ name: 'Browse All', icon: '🔍' }
	];

	const dishes = [
		{
			name: 'Fattoush salad',
			price: 24.0,
			rating: 4.9,
			image: 'https://i.pinimg.com/474x/54/f9/4d/54f94db34a347986d244bda6d6bc12b0.jpg?enhanced'
		},
		{
			name: 'Vegetable salad',
			price: 26.0,
			rating: 4.8,
			image: 'https://i.pinimg.com/236x/fc/2c/29/fc2c29a4af2dcb82ef3cdaf2768ac4d4.jpg?enhanced'
		},
		{
			name: 'Egg-plant salad',
			price: 23.0,
			rating: 4.7,
			image: 'https://i.pinimg.com/236x/e2/07/59/e20759c811677e3c1b6ba6404de87711.jpg?enhanced'
		}
	];

	const client = [
		{
			image: 'https://i.pinimg.com/236x/c3/16/81/c31681e9cb91fca8f585804973ca9ea7.jpg?enhanced'
		},
		{
			image: 'https://i.pinimg.com/236x/ae/59/47/ae5947515d90e8bcc0bc38869b2fa3e5.jpg?enhanced'
		},
		{
			image: 'https://i.pinimg.com/236x/6d/37/be/6d37be78016363cec5fd48d327b78cbe.jpg?enhanced'
		}
	];

	const services = [
		{
			icon: '🍽️',
			title: 'CATERING',
			description: 'Delight your guests with our flavors and presentation'
		},
		{
			icon: '⏰',
			title: 'FAST DELIVERY',
			description: 'We deliver your order promptly to your door'
		},
		{
			icon: '🛒',
			title: 'ONLINE ORDERING',
			description: 'Explore menu & order with ease using our Online Ordering'
		},
		{
			icon: '🎁',
			title: 'GIFT CARDS',
			description: 'Give the gift of exceptional dining with 飢え Gift Cards'
		}
	];
</script>

<div class="min-h-screen bg-white md:px-7">
	<!-- Header -->
	<header
		class="fixed left-0 right-0 top-0 z-50 border-b bg-white/95 backdrop-blur-sm"
		transition:slide={{ duration: 300, axis: 'y' }}
	>
		<nav class="container mx-auto flex h-16 items-center justify-between px-4">
			<a href="/" class="text-3xl font-bold tracking-widest text-green-500">飢え</a>

			<div class="hidden items-center gap-8 md:flex">
				<a href="/" class="transition-colors hover:text-green-500">Home</a>
				<a href="/" class="transition-colors hover:text-green-500">Menu</a>
				<a href="/" class="transition-colors hover:text-green-500">About</a>
				<a href="/" class="transition-colors hover:text-green-500">Contact</a>
			</div>

			<div class="flex items-center gap-4">
				{#if showSearch}
					<div transition:slide>
						<Input
							type="search"
							placeholder="Search..."
							bind:value={searchQuery}
							class="w-40 md:w-60"
						/>
					</div>
				{/if}
				<Button
					variant="ghost"
					size="icon"
					on:click={() => (showSearch = !showSearch)}
					class="hidden lg:flex"
				>
					<Search class="h-5 w-5" />
					<span class="sr-only">Search</span>
				</Button>
				<Button class="bg-green-500 hover:bg-green-600">Order Now</Button>
			</div>
		</nav>
	</header>

	<!-- Hero Section -->
	<section class="container mx-auto flex flex-col items-center gap-8 px-4 pb-16 pt-32 md:flex-row">
		{#if mounted}
			<div class="flex-1 space-y-7" in:fly={{ y: 50, duration: 1000, delay: 300 }}>
				<h1 class="text-4xl font-bold leading-tight md:text-6xl">
					Dive Into Delights Of Delectable <span class="text-green-500">Food</span>
				</h1>
				<p class="text-lg text-gray-600">
					Where every flavor tells a story. Experience the perfect blend of taste and tradition.
				</p>
				<div class="flex gap-4">
					<Button class="h-10 bg-green-500 hover:bg-green-600">Order Now</Button>
					<Button variant="outline" class="h-10 gap-2">
						Watch Video <ChevronRight class="h-4 w-4" />
					</Button>
				</div>
			</div>
			<div class="relative flex-1" in:fly={{ x: 50, duration: 1000, delay: 600 }}>
				<div class="absolute inset-0 scale-90 rounded-full bg-green-500 opacity-20 blur-3xl"></div>
				<img src={chef} alt="Chef preparing food" class="relative h-auto w-full" />
			</div>
		{/if}
	</section>

	<!-- Categories -->
	<section class="container mx-auto px-4 py-16">
		<h2 class="mb-8 text-2xl font-bold" in:fade={{ duration: 500 }}>Popular Categories</h2>
		<div class="flex flex-wrap justify-center gap-8">
			{#each categories as category, i}
				<div
					class="group flex cursor-pointer flex-col items-center gap-4"
					in:fly={{ y: 20, duration: 500, delay: 100 * i }}
				>
					<div
						class="flex h-24 w-24 items-center justify-center rounded-full bg-green-100 text-4xl
                        transition-all duration-300 group-hover:bg-green-500 group-hover:text-white"
					>
						{category.icon}
					</div>
					<span class="font-medium">{category.name}</span>
				</div>
			{/each}
		</div>
	</section>

	<!-- Dishes -->
	<section class="container mx-auto bg-gray-50 px-4 py-16">
		<h2 class="mb-2 text-2xl font-bold" in:fade={{ duration: 500 }}>Standout Dishes</h2>
		<p class="mb-8 text-gray-600" in:fade={{ duration: 500, delay: 200 }}>From Our Menu</p>
		<div class="flex flex-wrap justify-center gap-8">
			{#each dishes as dish, i}
				<Card
					class="group w-full transition-all duration-300 hover:scale-105 hover:shadow-lg md:w-72"
				>
					<img src={dish.image} alt={dish.name} class="h-48 w-full rounded-t-lg object-cover" />
					<div class="space-y-4 p-4">
						<div class="flex items-center justify-between">
							<h3 class="font-semibold">{dish.name}</h3>
							<Badge variant="outline" class="bg-green-50">
								<Star class="mr-1 h-4 w-4 text-yellow-400" />
								{dish.rating}
							</Badge>
						</div>
						<div class="flex items-center justify-between">
							<span class="text-lg font-bold">${dish.price.toFixed(2)}</span>
							<Button size="sm" class="bg-green-500 hover:bg-green-600">Add to Cart</Button>
						</div>
					</div>
				</Card>
			{/each}
		</div>
	</section>

	<section class="mx-auto max-w-7xl px-4 py-12">
		<!-- Testimonials Section -->
		<div class="mb-20 flex flex-col items-center gap-8 lg:flex-row">
			{#if mounted}
				<div
					class="relative ms-7 flex w-full max-w-md flex-1 justify-center md:ms-0 lg:max-w-none"
					in:fly={{ x: -50, duration: 1000, delay: 300 }}
				>
					<div class="relative -left-4 h-80 w-80 rounded-full bg-[#4ADE80] bg-opacity-20">
						<img
							src={chuck}
							alt="Professional chef"
							class="relative z-10 mx-auto mt-2 w-full max-w-sm rounded-b-full"
						/>
					</div>
				</div>

				<div
					class="mx-auto w-full max-w-md flex-1 lg:max-w-none"
					in:fly={{ x: 50, duration: 1000, delay: 600 }}
				>
					<p class="mb-2 font-medium text-red-500">TESTIMONIALS</p>
					<h2 class="mb-6 text-3xl font-bold lg:text-4xl">What Our Customers Say About Us</h2>

					<blockquote class="mb-8 text-gray-600">
						"I had the pleasure of dining at 飢え last night, and I'm still raving about the
						experience! The attention to detail in presentation and service was impeccable"
					</blockquote>

					<div class="flex items-center gap-4">
						<div class="flex -space-x-2">
							{#each Array(3) as _, i}
								<img
									src={client[i].image}
									alt="Customer"
									class="h-10 w-10 rounded-full border-2 border-white"
								/>
							{/each}
						</div>
						<div>
							<p class="font-semibold">Customer Feedback</p>
							<div class="flex items-center gap-1">
								<svg class="h-4 w-4 fill-current text-yellow-400" viewBox="0 0 24 24">
									<path
										d="M12 17.27L18.18 21l-1.64-7.03L22 9.24l-7.19-.61L12 2 9.19 8.63 2 9.24l5.46 4.73L5.82 21z"
									/>
								</svg>
								<span class="font-medium">4.9</span>
								<span class="text-sm text-gray-500">(18.6k Reviews)</span>
							</div>
						</div>
					</div>
				</div>
			{/if}
		</div>

		<!-- Services Section -->
		<div class="flex flex-col items-start gap-12 lg:flex-row">
			{#if mounted}
				<div
					class="mx-auto w-full max-w-md flex-1 lg:max-w-none"
					in:fly={{ x: -50, duration: 1000, delay: 300 }}
				>
					<p class="mb-2 font-medium text-red-500">OUR STORY & SERVICES</p>
					<h2 class="mb-6 text-3xl font-bold lg:text-4xl">Our Culinary Journey And Services</h2>
					<p class="mb-8 text-gray-600">
						Rooted in passion, we curate unforgettable dining experiences and offer exceptional
						services, blending culinary artistry with warm hospitality.
					</p>
					<button
						class="transform rounded bg-[#4ADE80] px-4 py-2 font-bold text-white transition duration-300 ease-in-out hover:scale-105 hover:bg-[#4ADE80]/90"
					>
						Explore
					</button>
				</div>

				<div class="w-full flex-1" in:fly={{ x: 50, duration: 1000, delay: 600 }}>
					<div class="grid grid-cols-1 gap-4 sm:grid-cols-2">
						{#each services as service, i}
							<div
								class="rounded-lg border p-6 shadow-sm transition-all duration-300 ease-in-out hover:shadow-lg"
								in:scale={{ duration: 500, delay: 200 * i, easing: elasticOut }}
							>
								<div
									class="mb-4 flex h-12 w-12 items-center justify-center rounded-full bg-[#4ADE80]/10"
								>
									<span class="text-2xl">{service.icon}</span>
								</div>
								<h3 class="mb-2 text-sm font-medium text-[#4ADE80]">{service.title}</h3>
								<p class="text-sm text-gray-600">{service.description}</p>
							</div>
						{/each}
					</div>
				</div>
			{/if}
		</div>
	</section>

	<!-- Footer -->
	<footer class="border-t bg-white" transition:fade={{ duration: 300 }}>
		<div class="container mx-auto px-4 py-8">
			<div class="flex flex-wrap justify-between gap-8">
				<div class="space-y-4">
					<h3 class="text-2xl font-bold text-green-500">飢え</h3>
					<p class="max-w-xs text-gray-600">
						Bringing the finest flavors to your table, one dish at a time.
					</p>
				</div>

				<div>
					<h4 class="mb-4 font-semibold">Quick Links</h4>
					<div class="space-y-2">
						<a href="/" class="block text-gray-600 hover:text-green-500">Home</a>
						<a href="/" class="block text-gray-600 hover:text-green-500">Menu</a>
						<a href="/" class="block text-gray-600 hover:text-green-500">About</a>
						<a href="/" class="block text-gray-600 hover:text-green-500">Contact</a>
					</div>
				</div>

				<div>
					<h4 class="mb-4 font-semibold">Contact Us</h4>
					<div class="space-y-2 text-gray-600">
						<p>+1234 8090 1234</p>
						<p>info@飢え.com</p>
						<p>123 飢え Street, NY</p>
					</div>
				</div>

				<div>
					<h4 class="mb-4 font-semibold">Follow Us</h4>
					<div class="flex gap-4">
						<Button
							variant="ghost"
							size="icon"
							class="rounded-full hover:bg-[#4ADE80] hover:text-white"
						>
							<Facebook class="h-5 w-5" />
							<span class="sr-only">Facebook</span>
						</Button>
						<Button
							variant="ghost"
							size="icon"
							class="rounded-full hover:bg-[#4ADE80] hover:text-white"
						>
							<Twitter class="h-5 w-5" />
							<span class="sr-only">Twitter</span>
						</Button>
						<Button
							variant="ghost"
							size="icon"
							class="rounded-full hover:bg-[#4ADE80] hover:text-white"
						>
							<Instagram class="h-5 w-5" />
							<span class="sr-only">Instagram</span>
						</Button>
					</div>
				</div>
			</div>

			<div class="mt-8 border-t pt-8 text-center text-gray-600">
				<p>&copy; {new Date().getFullYear()} 飢え. 無断転載を禁じます。</p>
			</div>
		</div>
	</footer>
</div>

<style>
	:global(html) {
		scroll-behavior: smooth;
	}
</style>
