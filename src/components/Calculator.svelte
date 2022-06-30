<style lang="scss">
    .calculator {
        display: flex;
        flex-flow: column;
        align-items: center;
        background-color: white;
        border-radius: 15px;
        color: #333;
        font-size: 20px;
        padding: 20px;
        margin: 0 5%;
    }

    .result {
        font-size: 30px;
    }

    .buttons {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        width: 100%;
        margin-top: 20px;
    }

    .number, .subtract {
        border: unset;
        background-color: #dddddd;
        border-radius: 12px;
        max-height: 40px;
    }

    .number,.delete, .subtract {
        margin: 0 .5em .5em;
    }

    .number:active {
        background-color: #b6b6b6;
    }

    .subtract {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .delete {
        border: unset;
        background: unset;

        & > img {
            transform: scale(1.5);
        }
    }

    .actions {
        display: flex;
        justify-content: space-evenly;
        width: 100%;

        & > button {
            margin-top: 10px;
            width: 45%;
            border-radius: 12px;
        }
    }

    .cancel {
        background-color: unset;
        border-width: 4px;
    }

    .save, .active {
        border: unset;
        background-color: #3c3cff;
        color: #ffffff;
    }
</style>

<script lang="ts">
    export let life: number;
    export let showCalculator: boolean;

    let subtract = false;
    let result = '0';

    $: modifier = subtract ? '-' : '+';

    const update = (e: Event) => {
        const element = e.currentTarget as HTMLElement;
        const number = element.textContent;
        
        if (result === '0') result = number
        else result = result + number;
    }

    const save = () => {
        life = subtract ? life - parseInt(result, 10) : life + parseInt(result, 10);
        showCalculator = false;
    };

    const deleteChar = () => {
        if (result === '0') return;
        else if (result.length === 1) result = '0';
        else result = result.slice(0, -1);
    }

    const hideCalc = () => showCalculator = false;
    const toggleSubtract = () => subtract = !subtract;
</script>

<div class="calculator">
    <div class="result">
        <span>{modifier}</span>
        <span class="result">{result}</span>
    </div>
    <div class="buttons">
        <button on:click={update} class="number">1</button>
        <button on:click={update} class="number">2</button>
        <button on:click={update} class="number">3</button>
        <button on:click={update} class="number">4</button>
        <button on:click={update} class="number">5</button>
        <button on:click={update} class="number">6</button>
        <button on:click={update} class="number">7</button>
        <button on:click={update} class="number">8</button>
        <button on:click={update} class="number">9</button>
        <button on:click={toggleSubtract} class="subtract" class:active={subtract}> - </button>
        <button on:click={update} class="number">0</button>
        <button on:click={deleteChar} class="delete"><img src="/assets/delete.svg" alt="delete"></button>
    </div>
    <div class="actions">
        <button on:click={hideCalc} class="cancel">Cancel</button>
        <button on:click={save} class="save">Update</button>
    </div>
</div>