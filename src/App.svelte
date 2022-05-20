<style>
	main {
		width: 100%;
		height: 100%;
		display: flex;
		flex-flow: column;
		justify-content: space-between;
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

	.fullscreen-toggle {
		position: fixed;
		z-index: 10;
		padding: 10px;
		filter: invert();
	}
</style>

<script lang="ts">
	import LifeCounter from "./components/LifeCounter.svelte";
	import CommanderDamage from "./components/CommanderDamage.svelte";
	import Calculator from './components/Calculator.svelte';

	let life = 40;
	let showCalculator = false;
	let isFullscreen = false;
	
	const increase = () => life++;
	const decrease = () => life--;
	const toggleFullscreen = () => {
		if (isFullscreen) {
			document.exitFullscreen().then(() => isFullscreen = false);
			return;
		}

		document.querySelector('body').requestFullscreen().then(() => isFullscreen = true);
	}
</script>

<main>
	{#if document.fullscreenEnabled}
	<span class="fullscreen-toggle" on:click={toggleFullscreen}>
		{#if isFullscreen}
			<img src="/assets/minimize.svg" alt="Exit Fullscreen">
		{:else}
			<img src="/assets/maximize.svg" alt="Enter Fullscreen">
		{/if}
	</span>
	{/if}
	<div class="commander-damage">
		<CommanderDamage increaseLife={increase} decreaseLife={decrease} />
		<CommanderDamage increaseLife={increase} decreaseLife={decrease} />
		<CommanderDamage increaseLife={increase} decreaseLife={decrease} />
		<CommanderDamage increaseLife={increase} decreaseLife={decrease} />
		<CommanderDamage increaseLife={increase} decreaseLife={decrease} />
	</div>
	<div class="life-counter">
		<LifeCounter life={life} increase={increase} decrease={decrease} showModal={() => showCalculator = true} />
	</div>

	{#if showCalculator}
	<div class="modal">
		<div class="life-calc">
			<Calculator currentLife={life} hide={() => showCalculator = false} update={(newLife) => life = newLife} />
		</div>
	</div>
	{/if}
</main>