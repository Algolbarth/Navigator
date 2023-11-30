<script>
    import Tree from "./Tree.svelte";
    export let System;
    export let Stockage;
    export let Path;
    export let move;
    export let tab;
    System;
    Stockage;
    Path;
    move;
    tab;

    function newpath() {
        let path = [];
        for (let i=0;i<Path.length;i++) {
            path.push(Path[i]);
        }
        path.push(Stockage);
        return path;
    } 
</script>

<div style={"margin-left:" + 1.5*tab + "vw;"}>
    <button on:click={() => {move(Stockage, newpath())}}>
        <img src="Pictures/folder.svg" alt="icon"/> 
        {#if System.currentFolder == Stockage}
            <div style="display:inline;color:red">{Stockage.name}</div>
        {:else}
            {Stockage.name}
        {/if}
    </button>
    {#if Stockage.folders.length > 0}
        {#each Stockage.folders as folder, i}
            <svelte:component this={Tree} {System} Stockage={folder} Path={newpath()} {move} tab={tab+1}/>
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