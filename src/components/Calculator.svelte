<style>
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

    .number {
        border: unset;
        background-color: #cecece;
        border-radius: 12px;
        max-height: 40px;
    }

    .number,.delete {
        margin: 0 .5em .5em;
    }

    .number.last {
        grid-column: 2;
    }

    .delete {
        border: unset;
        background: unset;
    }

    .delete > img {
        transform: scale(1.5);
    }

    .actions {
        display: flex;
        justify-content: space-evenly;
        width: 100%;
    }

    .actions > button {
        margin-top: 10px;
        width: 45%;
        border-radius: 12px;
    }

    .cancel {
        background-color: unset;
        border-width: 4px;
    }

    .save {
        border: unset;
        background-color: #3c3cff;
        color: #ffffff;
    }
</style>

<script lang="ts">
    import '@fortawesome/fontawesome-free/css/all.min.css'

    export let hide: () => void;
    export let update: (life: number) => void;   

    let result = '0';

    const updateResult = (number: string) => {
        if (result === '0') result = number
        else result = result + number;
    }

    const save = () => {
        update(parseInt(result, 10));
        hide();
    };

    const deleteChar = () => {
        if (result === '0') return;
        else if (result.length === 1) result = '0';
        else result = result.slice(0, -1);
    }
</script>

<div class="calculator">
    <span class="result">{result}</span>
    <div class="buttons">
        <button on:click={() => updateResult('1')} class="number">1</button>
        <button on:click={() => updateResult('2')} class="number">2</button>
        <button on:click={() => updateResult('3')} class="number">3</button>
        <button on:click={() => updateResult('4')} class="number">4</button>
        <button on:click={() => updateResult('5')} class="number">5</button>
        <button on:click={() => updateResult('6')} class="number">6</button>
        <button on:click={() => updateResult('7')} class="number">7</button>
        <button on:click={() => updateResult('8')} class="number">8</button>
        <button on:click={() => updateResult('9')} class="number">9</button>
        <button on:click={() => updateResult('0')} class="number last">0</button>
        <button on:click={deleteChar} class="delete"><img src="/assets/delete.svg" alt="delete"></button>
    </div>
    <div class="actions">
        <button on:click={hide} class="cancel">Cancel</button>
        <button on:click={save} class="save">Set</button>
    </div>
</div>