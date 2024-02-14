<script>
    import Typewriter from "./Typewriter.svelte";

    let NewLineV;

    let Divs = [];
    let DivCount = 0;

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

    function LineInit() {
        if (Divs.length == 0) {
            AddDiv();
        }
    }

    function CreateNewLine() {
        if (NewLineV) {
            NewLineV = false;
            AddDiv();
        }
    }

    $: {
        LineInit();
        CreateNewLine();
    }
</script>

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

<style>
    .typewriter-container {
        width: 50%;
        height: 100%;
        margin: auto;
        background-color: gray;
        padding: 3%;
        border-radius: 10px;
    }
    .typewriter {
        background-color: darkgray;
        border-radius: 5px;
        padding: 3%;
        margin-top: 1%;
    }
    .flex-center {
        display: flex;
        justify-content: center;
        flex-direction: column;
    }
</style>
