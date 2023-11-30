<script>
    import Tree from "./Tree.svelte";
    export let System;
    System;
    
    export function move (folder, path) {
        System.currentFolder = folder;
        sort(System.currentFolder.folders);
        sort(System.currentFolder.links);
        System.path = path;
        System.pages.change("Menu");
    };

    function sort (tab) {
        for (let i=0;i<tab.length;i++) {
            let j = i;
            while (j > 0 && tab[j].name < tab[j-1].name) {
                let swap = tab[j-1];
                tab[j-1] = tab[j];
                tab[j] = swap;
                j--;
            }
        }
    };
</script>

<div>
    <button on:click={() => {System.pages.change("Menu")}}>Annuler</button>
    <br/>
    <svelte:component this={Tree} {System} Stockage={System.folders[0]} Path={[]} {move} tab={0} />
</div>

<style>
    div {
        text-align:left;
    }
</style>