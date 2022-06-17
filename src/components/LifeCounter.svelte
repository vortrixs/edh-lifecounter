<style>
    .life-wrapper {
        width: inherit;
        height: 100%;
        display: flex;
        gap: 10px;
        align-items: center;
        justify-content: center;
    }

    .counters {
        z-index: 0;
        display: flex;
        flex-flow: column;
        align-items: center;
    }

    .ticker {
        position: fixed;
        font-size: 20px;
        font-weight: 700;
    }

    .ticker.positive {
        color: #46d846;
    }

    .ticker.negative {
        color: #d84646;
    }

    .ticker.hidden {
        display: none;
    }

    .life {
        font-size: 80px;
    }

    .life.dead {
        color: #d84646;
    }

    .increase {
        right: 0;
    }

    .decrease {
        left: 0;
    }

    .increase, .decrease {
        z-index: 1;
        position: fixed;
        bottom: 0;
        background-color: transparent;
        border: unset;
        width: 35%;
        height: 50%;
    }

    :is(.increase, .decrease):active {
        background-color: hsl(0, 0%, 22%);
        opacity: .5;
    }
</style>

<script lang="ts">
    export let life: number;
    export let showCalculator: boolean;

    let timeout: NodeJS.Timeout;
    let ticker = 0;
    
    $: lifeTick = (ticker <= 0 ? '' : '+') + ticker;
    $: hidden = ticker === 0;
    $: positive = ticker > 0;
    $: negative = ticker < 0;
    $: dead = life <= 0;

    const increase = () => {
        life++;
        ticker++;
        clearTimeout(timeout);
        timeout = setTimeout(() => ticker = 0, 2000)
    }

    const decrease = () => {
        life--;
        ticker--;
        clearTimeout(timeout);
        timeout = setTimeout(() => ticker = 0, 2000)
    }

    const showCalc = () => showCalculator = true;
</script>

<div class="life-wrapper">
    <button class="decrease" on:click={decrease}/>
    <div class="counters">
        <p class="ticker" class:hidden class:positive class:negative>{lifeTick}</p>
        <p class="life" class:dead on:click={showCalc}>{life}</p>
    </div>
    <button class="increase" on:click={increase}/>
</div>