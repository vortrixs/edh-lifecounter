<style>
    .fullscreen-toggle {
		display: flex;
		padding-left: 10px;
	}

	.fullscreen-toggle > img {
		filter: invert();
	}
</style>

<script>
	const bodyRef = document.querySelector('body');
	let isFullscreen = false;

	const toggleFullscreen = () => isFullscreen ? document.exitFullscreen() : bodyRef.requestFullscreen();

	new ResizeObserver((entries) => {
		const contentHeight = entries[0].contentRect.height;

		if (contentHeight < window.outerHeight) {
			isFullscreen = false;
		} else if (contentHeight === window.outerHeight) {
			isFullscreen = true;
		}
	}).observe(bodyRef);
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