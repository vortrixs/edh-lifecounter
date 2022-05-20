<style>
    .battery-indicator {
        position: fixed;
        right: 0;
        padding: 15px;
    }

    .battery-indicator > img {
        filter: invert();
    }
</style>

<script>
    let batteryLevel = null;

    const levels = {
        charging: '/assets/battery-charging.svg',
        empty: '/assets/battery.svg',
        25: '/assets/battery_25.svg',
        50: '/assets/battery_50.svg',
        75: '/assets/battery_75.svg',
        100: '/assets/battery_100.svg',
    }
</script>

<div class="battery-indicator">
    <img src={levels.charging} alt="Battery charging">
    <img src={levels.empty} alt="Battery empty">
    <img src={levels[25]} alt="Battery 25%">
    <img src={levels[50]} alt="Battery 50%">
    <img src={levels[75]} alt="Battery 75%">
    <img src={levels[100]} alt="Battery 100%">
</div>