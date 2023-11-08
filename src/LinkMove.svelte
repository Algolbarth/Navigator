<script>
    import Tree from "./Tree.svelte";
    export let System;
    System;
    
    export function move (folder) {
        for (let i=0;i<System.currentFolder.links.length;i++) {
            if (System.currentFolder.links[i] == System.edit) {
                System.currentFolder.links.splice(i, 1);
            }
        }
        folder.links.push(System.edit);
        System.pages.change("Menu");
    };
</script>

<div>
    <button on:click={() => {System.pages.change("LinkEdit")}}>Annuler</button>
    <br/>
    <svelte:component this={Tree} {System} Stockage={System.folders[0]} {move} tab={0} />
</div>

<style>
    div {
        text-align:left;
    }
</style>