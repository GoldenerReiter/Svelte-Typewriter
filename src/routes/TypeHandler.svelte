<script>
    import { tick } from "svelte";
    import Typewriter from "./Typewriter.svelte";

    // Variables extracted from the child component
    let NewLineV = false;

    // Div variables for AddDiv function
    let Divs = [];
    let DivCount = 0;

    // Creates a new Div with its properties originary put to false
    function AddDiv() {
        DivCount += 1;
        Divs = [
            ...Divs,
            {
                id: DivCount,
                IsWrittenV: false,
                NewLineV: false,
                FullfilledV: false,
            },
        ];
    }

    // When the program starts, it creates a div automatically if there is not
    function LineInit() {
        if (Divs.length == 0) {
            AddDiv();
        }
    }

    // Reactively checks if there is any Div or there is a requirement for a new line
    $: {
        LineInit();
        if (NewLineV) {
            NewLineV = false;
            AddDiv();
        }
    }
</script>

<!-- Div rendering if there is any -->
{#if Divs.length > 0}
    <div class="typewriter-container flex-center">
        {#each Divs as Div}
            <div class="typewriter flex-center">
                <Typewriter
                    bind:IsWritten={Div.IsWrittenV}
                    bind:NewLine={NewLineV}
                    bind:Fullfilled={Div.FullfilledV}
                />
            </div>
        {/each}
    </div>
    <!-- If there is not, you get an error message -->
{:else}
    <p>Something went wrong!</p>
{/if}

<style>
    .typewriter-container {
        width: 50%;
        height: 100%;
        margin: auto;
        background-color: gray;
        border-radius: 10px;
    }
    .typewriter {
        background-color: darkgray;
        border-radius: 5px;
        margin-top: 1%;
    }
    .flex-center {
        display: flex;
        justify-content: center;
        flex-direction: column;
        padding: 3%;
    }
</style>
