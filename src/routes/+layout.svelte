<script>
	import Icon from '@iconify/svelte';
	import '../app.css';
	import { fav } from './store.js';
	import { page, navigating } from '$app/stores';
	import { onMount, onDestroy } from 'svelte';
	import { navigate } from 'svelte-routing';

	const navs = [
		{ name: 'LUGGAGE', href: 'luggage' },
		{ name: 'BACKPACK', href: 'backpack' },
		{ name: 'SHOULDER BAG', href: 'shoulder_bag' },
		{ name: 'ACCESSORIES', href: 'accessories' }
	];
	let favSubscription;
	onMount(() => {
		favSubscription = fav.subscribe((value) => {
			if ($fav) {
				navigate('/favorite');
			} else {
				window.history.back();
			}
		});
	});
	onDestroy(() => {
		if (favSubscription) {
			favSubscription;
		}
	});
</script>

<nav
	class="absolute w-screen bg-slate-800 bg-opacity-10 flex flex-row justify-between py-10 px-28 items-center"
>
	<a href="/" aria-current={$page.url.pathname === '/'} class="text-4xl text-white font-semibold"
		>Krapaw</a
	>
	<div class="flex flex-row gap-10">
		{#each navs as nav}
			<a
				href="/{nav.href}"
				aria-current={$page.url.pathname === `/${nav.href}`}
				class="text-xl text-white">{nav.name}</a
			>
		{/each}
		<button class="text-2xl text-white" on:click={() => fav.update((n) => !n)}>
			{#if $fav}
				<Icon icon="flowbite:star-solid" />
			{:else}
				<Icon icon="flowbite:star-outline" />
			{/if}
		</button>
	</div>
</nav>
<slot />
