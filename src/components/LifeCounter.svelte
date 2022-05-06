<style>
    .life-wrapper {
        display: flex;
        gap: 10px;
    }
</style>

<script lang="ts">
    export let life: number;
    export let increase: () => void;
    export let decrease: () => void;
    export let showModal: () => void;
</script>

<div class="life-wrapper">
    <button on:click={decrease}/>
    <p on:click={showModal}>{life}</p>
    <button on:click={increase}/>
</div>