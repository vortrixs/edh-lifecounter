<style>
    .life-wrapper {
        width: inherit;
        height: 100%;
        display: flex;
        gap: 10px;
        align-items: center;
    }

    .counters {
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

    .increase, .decrease {
        background-color: transparent;
        border: unset;
        width: 100%;
        height: 100%;
    }

    :is(.increase, .decrease):active {
        background-color: hsl(0, 0%, 21%);
    }
</style>

<script lang="ts">
    export let life: number;
    export let increase: () => void;
    export let decrease: () => void;
    export let showModal: () => void;

    let timeout: NodeJS.Timeout;

    const increaseLife = () => {
        increase();
        ticker++;
        clearTimeout(timeout);
        timeout = setTimeout(() => ticker = 0, 2000)
    }

    const decreaseLife = () => {
        decrease();
        ticker--;
        clearTimeout(timeout);
        timeout = setTimeout(() => ticker = 0, 2000)
    }

    let ticker = 0;

    $: lifeTick = (ticker<=0?"":"+") + ticker;
    $: isDead = life <= 0;

    $: tickerClasses = [
        'ticker',
        ticker === 0 ? 'hidden' : '',
        ticker > 0 ? 'positive' : '',
        ticker < 0 ? 'negative' : '',
    ];
</script>

<div class="life-wrapper">
    <button class="decrease" on:click={decreaseLife}/>
    <div class="counters">
        <p class={tickerClasses.join(' ').trim()}>{lifeTick}</p>
        <p class="life {isDead ? 'dead' : ''}" on:click={showModal}>{life}</p>
    </div>
    <button class="increase" on:click={increaseLife}/>
</div>