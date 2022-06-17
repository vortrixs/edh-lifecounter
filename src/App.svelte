<style>
	main {
		width: 100%;
		height: 100%;
		display: flex;
		flex-flow: column;
		justify-content: space-between;
	}

	.header {
		position: fixed;
		z-index: 10;
		width: 100%;
		
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding-top: 10px;
	}

	.commander-damage {
		height: 50%;
		display: flex;
		justify-content: space-evenly;
		align-items: center;
	}

	.life-counter {
		width: 100%;
		height: 50%;
		display: flex;
	}

	.modal {
		z-index: 9999;
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: black;
	}

	.life-calc {
		display: flex;
		flex-flow: column;
		width: inherit;
		height: inherit;
		justify-content: center;
	}
</style>

<script context="module">
	// @ts-ignore
	const hasBatteryApiSupport = typeof navigator.getBattery !== 'undefined';
</script>

<script lang="ts">
	import LifeCounter from "./components/LifeCounter.svelte";
	import CommanderDamage from "./components/CommanderDamage.svelte";
	import Calculator from './components/Calculator.svelte';
	import Fullscreen from './components/Fullscreen.svelte'
	import Battery from './components/Battery.svelte'

	export let life = 40;
	export let showCalculator = false;
</script>

<main>
	<div class="header">
		<Fullscreen />
		{#if hasBatteryApiSupport }
			<Battery />
		{/if}
	</div>
	<div class="commander-damage">
		<CommanderDamage bind:life />
		<CommanderDamage bind:life />
		<CommanderDamage bind:life />
		<CommanderDamage bind:life />
		<CommanderDamage bind:life />
	</div>
	<div class="life-counter">
		<LifeCounter bind:life bind:showCalculator />
	</div>
</main>
{#if showCalculator}
<div class="modal">
	<div class="life-calc">
		<Calculator bind:life bind:showCalculator />
	</div>
</div>
{/if}