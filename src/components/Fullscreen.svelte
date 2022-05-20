<style>
    .fullscreen-toggle {
		position: fixed;
		z-index: 10;
		padding: 10px;
		filter: invert();
	}
</style>

<script>
	let isFullscreen = false;

    const toggleFullscreen = () => {
		if (isFullscreen) {
			document.exitFullscreen().then(() => isFullscreen = false);
			return;
		}

		document.querySelector('body').requestFullscreen().then(() => isFullscreen = true);
	}
</script>

{#if document.fullscreenEnabled}
<span class="fullscreen-toggle" on:click={toggleFullscreen}>
    {#if isFullscreen}
        <img src="/assets/minimize.svg" alt="Exit Fullscreen">
    {:else}
        <img src="/assets/maximize.svg" alt="Enter Fullscreen">
    {/if}
</span>
{/if}