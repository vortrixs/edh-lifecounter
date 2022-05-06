<style>
    .life-wrapper {
        width: inherit;
        height: 100%;
        display: flex;
        gap: 10px;
        align-items: center;
    }

    .life {
        font-size: 80px;
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
</script>

<div class="life-wrapper">
    <button class="decrease" on:click={decrease}/>
    <p class="life" on:click={showModal}>{life}</p>
    <button class="increase" on:click={increase}/>
</div>