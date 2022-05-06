<style>
	.commander-damage {
		display: flex;
		justify-content: space-evenly;
	}

	.life-counter {
		margin-top: 50px;
		display: flex;
		justify-content: center;
	}

	.life-calc {
		z-index: 9999;
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		padding-top: 50%;
		background-color: black;
	}
</style>

<script lang="ts">
	import LifeCounter from "./components/LifeCounter.svelte";
	import CommanderDamage from "./components/CommanderDamage.svelte";
	import Calculator from './components/Calculator.svelte';

	let life = 40;
	let showCalculator = false;
	const increase = () => life++;
	const decrease = () => life--;
</script>

<main>
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
		<div class="life-calc"><Calculator hide={() => showCalculator = false} update={(newLife) => life = newLife} /></div>
	{/if}
</main>