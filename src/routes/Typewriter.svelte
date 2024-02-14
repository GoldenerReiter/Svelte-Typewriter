<script>
    import { writable } from "svelte/store";

    let Typewriter = writable("Insert your text here...");

    export let NewLine = false;
    export let IsWritten = false;
    export let Fullfilled = false;

    $: if (Typewriter != "Insert your text here...") {
        IsWritten = true;
    }
</script>
<!-- Rendering of the input -->
<p>{$Typewriter}</p>
<!-- Input if there is not a requirement for a new line -->
{#if NewLine === false && Fullfilled === false}
    <input bind:value={$Typewriter} />
{/if}
<!-- If there is  -->
{#if IsWritten}
    <input
        class="submit"
        type="submit"
        on:click={() => {
            NewLine = true;
            IsWritten = false;
            Fullfilled = true;
        }}
    />
{/if}

<style>
    p {
        background-color: darkgray;
        margin: 1%;
        font-family: "Playfair Display", serif;
        font-optical-sizing: auto;
        font-weight: 400;
        font-style: normal;
    }
    input {
        background-color: azure;
        border-radius: 2px;
    }
    .submit {
        margin-top: 1%;
    }
</style>
