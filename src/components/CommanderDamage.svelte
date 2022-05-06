<style>
    .counter-wrapper {
        display: flex;
        flex-flow: column;
        align-items: center;
    }

    .damage {
        font-size: 30px;
        margin: 5px 0;
    }

    .damage.dead {
        color: #d84646;
    }

    .decrease > img {
        transform: translateY(1px);
    }

    .increase, .decrease {
        border-color: unset;
        border-radius: 50%;
        width: 40px;
        height: 40px;
        background-color: #dddddd;
    }

    :is(.increase, .decrease):active {
        background-color: #5f5f5f;
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

    $: isDead = damage === 21;
</script>

<div class="counter-wrapper">
    <button class="increase" on:click={increase}><img src="/assets/chevron-up.svg" alt="increase life"></button>
    <span class="damage {isDead ? 'dead' : ''}">{damage}</span>
    <button class="decrease" on:click={decrease}><img src="/assets/chevron-down.svg" alt="decrease life"></button>
</div>