<script>
    import Tree from "./Tree.svelte";
    export let System;
    export let Stockage;
    export let move;
    export let tab;
    System;
    Stockage;
    move;
    tab;
</script>

<div style={"margin-left:" + 1.5*tab + "vw;"}>
    <button on:click={() => {move(Stockage)}}>
        <img src="Pictures/folder.svg" alt="icon"/> 
        {#if System.currentFolder == Stockage}
            <div style="display:inline;color:red">{Stockage.name}</div>
        {:else}
            {Stockage.name}
        {/if}
    </button>
    {#if Stockage.folders.length > 0}
        {#each Stockage.folders as folder, i}
            <svelte:component this={Tree} {System} Stockage={folder} {move} tab={tab+1}/>
        {/each}
    {/if}
</div>

<style>
    button {
        border:none;
        background:none;
        font-weight: bold;
        margin:0;
        padding:0;
        cursor:pointer;
    }

    img {
        width:1.5vw;
    }
</style>