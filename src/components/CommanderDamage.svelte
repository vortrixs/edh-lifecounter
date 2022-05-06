<style>
    .counter-wrapper {
        display: flex;
        flex-flow: column;
        align-items: center;
    }
</style>

<script lang="ts">
    export let increaseLife: () => void;
    export let decreaseLife: () => void;

    let damage = 0;

    const increase = () => {
        if (damage < 21) {
            damage++;
            decreaseLife()
        }
    }

    const decrease = () => {
       if (damage > 0) {
           damage--;
           increaseLife()
        }
    }
</script>

<div class="counter-wrapper">
    <button class="inc" on:click={increase}> + </button>
    <p>{damage}</p>
    <button class="dec" on:click={decrease}> - </button>
</div>