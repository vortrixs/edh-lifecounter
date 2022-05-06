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
</main>
{#if showCalculator}
<div class="modal">
	<div class="life-calc">
		<Calculator hide={() => showCalculator = false} update={(newLife) => life = newLife} />
	</div>
</div>
{/if}