<style>
    .fullscreen-toggle {
		display: flex;
		padding-left: 10px;
	}

	.fullscreen-toggle > img {
		filter: invert();
	}
</style>

<script lang="ts">
	const bodyRef = document.querySelector('body');
	let isFullscreen = false;

	const toggleFullscreen = () => {
		if (isFullscreen) document.exitFullscreen().then(() => isFullscreen = false)
		else bodyRef.requestFullscreen().then(() => isFullscreen = true)
	};

	new ResizeObserver((entries) => {
		const contentHeight = entries[0].contentRect.height;
		
		if (contentHeight < window.outerHeight) isFullscreen = false;
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