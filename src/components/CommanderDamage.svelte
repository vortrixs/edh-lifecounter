<style lang="scss">
    .counter-wrapper {
        display: flex;
        flex-flow: column;
        align-items: center;
    }

    .damage {
        font-size: 30px;
        margin: 15px 0;

        &.dead {
            color: #d84646;
        }
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
        margin: 0;

        &:active {
            background-color: #b6b6b6;
        }
    }
</style>

<script lang="ts">
    export let life: number;

    let damage = 0;

    $: dead = damage === 21;

    const increase = () => {
        if (damage < 21) {
            damage++;
            life--;
        }
    }

    const decrease = () => {
       if (damage > 0) {
           damage--;
           life++;
        }
    }
</script>

<div class="counter-wrapper">
    <button class="increase" on:click={increase}><img src="/assets/chevron-up.svg" alt="increase life"></button>
    <span class="damage" class:dead>{damage}</span>
    <button class="decrease" on:click={decrease}><img src="/assets/chevron-down.svg" alt="decrease life"></button>
</div>