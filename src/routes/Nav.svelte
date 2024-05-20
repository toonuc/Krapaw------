<script>
	import Icon from '@iconify/svelte';
	import { writable } from 'svelte/store';
	const navs = ['luggage', 'backpack', 'shoulder bag', 'accessories'];
	let fav = writable(false);
</script>

<div class="absolute w-screen flex flex-row justify-between py-10 px-28 items-center">
	<div class="text-4xl text-white">Krapaw</div>
	<div class="flex flex-row gap-10">
		{#each navs as nav}
			<a href="/{nav}" class="text-xl text-white">{nav.toUpperCase()}</a>
		{/each}
		<button class="text-2xl text-white" on:click={() => fav.update(n => !n)}>
			{#if $fav}
				<Icon icon="flowbite:star-solid" />
			{:else}
				<Icon icon="flowbite:star-outline" />
			{/if}
        </button>
	</div>
</div>