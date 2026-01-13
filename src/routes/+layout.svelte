<script lang="ts">
	import { page } from '$app/state';
	import { locales, localizeHref, getLocale } from '$lib/paraglide/runtime';
	import { m } from '$lib/paraglide/messages.js';
	import './layout.css';
	import favicon from '$lib/assets/favicon.png';
	import Text from '$lib/text/Text.svelte';
	import LineBreak from '$lib/decorations/LineBreak.svelte';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<title>nulqwy</title>
</svelte:head>

<div class="flex h-full flex-col p-5 font-mono" style="justify-content:space-between">
	<div class="w-full">
		<div class="grow xl:mx-auto xl:max-w-7xl">
			{@render children()}
		</div>
	</div>

	<footer class="min-h-4 p-5 text-center">
		<LineBreak><Text>{m.slogan()}</Text></LineBreak>
		<div class="mx-auto flex justify-center gap-10">
			{#snippet localeLink(href: string, locale: string, name: string)}
				<Text>
					{#if getLocale() != locale}
						<a data-sveltekit-reload class="underline hover:italic" {href}>{name}</a>
					{:else}
						<span class="font-bold">{name}</span>
					{/if}
				</Text>
			{/snippet}

			{@render localeLink('/', 'en', 'english')}
			{@render localeLink('/uk', 'uk', 'українська')}
		</div>
	</footer>
</div>

<div style="display:none">
	{#each locales as locale}
		<a href={localizeHref(page.url.pathname, { locale })}>
			{locale}
		</a>
	{/each}
</div>
