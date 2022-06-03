<style>
    .battery-indicator {
        display: flex;
        align-items: center;
        gap: 5px;
        padding-right: 10px;
    }

    .battery-indicator > img {
        filter: brightness(0) invert(1);
    }

    .percentage {
        font-size: 12px;
    }

    .percentage.low {
        color: #f8454e;
    }
</style>

<script>
    const levels = {
        charging: {src:'/assets/battery-charging.svg',alt:'Battery charging'},
        empty: {src:'/assets/battery.svg',alt:'Battery empty'},
        p25: {src:'/assets/battery_25.svg',alt:'Battery 25%'},
        p50: {src:'/assets/battery_50.svg',alt:'Battery 50%'},
        p75: {src:'/assets/battery_75.svg',alt:'Battery 75%'},
        p100: {src:'/assets/battery_100.svg',alt:'Battery 100%'},
    }

    let level = levels.empty;
    let level_percentage = 0;

    navigator.getBattery().then((battery) => {
        const updateChargeInfo = () => {
            const actualLevel = battery.level*100;
            level_percentage = actualLevel;

            if (battery.charging) {
                level = levels.charging;
            } else {
                if (actualLevel>75) level = levels.p100;
                else if (actualLevel>50) level = levels.p75;
                else if (actualLevel>25) level = levels.p50;
                else if (actualLevel>10) level = levels.p25;
                else level = levels.empty;
            }
        }

        updateChargeInfo();
        battery.addEventListener('chargingchange', updateChargeInfo);
        battery.addEventListener('levelchange', updateChargeInfo);
    });    
</script>

<div class="battery-indicator">
    <span class="percentage" class:low={level_percentage<10}>{level_percentage}%</span><img {...level}>
</div>