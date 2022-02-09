<script lang="ts">
	import { onMount } from 'svelte';
	import TopAppBar, {
		Row,
		Section,
		Title,
		AutoAdjust,
		TopAppBarComponentDev
	} from '@smui/top-app-bar';
	import IconButton, { Icon } from '@smui/icon-button';
	import { mdiMenu, mdiWeatherSunny, mdiWeatherNight } from '@mdi/js';
	import { Svg } from '@smui/common/elements';

	let topAppBar: TopAppBarComponentDev;

	let darkTheme: boolean | undefined = undefined;

	onMount(() => {
		darkTheme = window.matchMedia('prefers-color-scheme: dark');
	});
</script>

<svelte:head>
	<!-- SMUI Styles -->
	{#if darkTheme === undefined}
		<link rel="stylesheet" href="/smui.css" media="(prefers-color-scheme: light)" />
	{:else if darkTheme}
		<link rel="stylesheet" href="/smui.css" />
		<link rel="stylesheet" href="/smui-dark.css" />
	{:else}
		<link rel="stylesheet" href="/smui.css" />
	{/if}
</svelte:head>

<TopAppBar bind:this={topAppBar} variant="standard">
	<Row>
		<Section>
			<IconButton>
				<Icon component={Svg} viewBox="0 0 24 24">
					<path fill="currentColor" d={mdiMenu} />
				</Icon>
			</IconButton>
			<Title>Standard</Title>
		</Section>
		<Section align="end" toolbar>
			<IconButton
				on:click={() => (darkTheme = !darkTheme)}
				title={darkTheme ? 'Lights on' : 'Lights off'}
				><Icon component={Svg} viewBox="0 0 24 24">
					<path fill="currentColor" d={darkTheme ? mdiWeatherSunny : mdiWeatherNight} />
				</Icon></IconButton
			>
		</Section>
	</Row>
</TopAppBar>
<AutoAdjust {topAppBar}>
	<slot />
</AutoAdjust>

<style>
	/* Hide everything above this component. */
	:global(app),
	:global(body),
	:global(html) {
		display: block !important;
		height: auto !important;
		width: auto !important;
		position: static !important;
	}
</style>
