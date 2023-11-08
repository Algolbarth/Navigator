<script>
    import Tree from "./Tree.svelte";
    export let System;
    System;
    
    export function copy (link) {
        copyLink(System.edit, link);
        System.pages.change("Menu");
    };

    function copyLink (link, emplacement) {
        let newLink = {
            name: link.name,
            url: link.url,
            icon: link.icon,
            icon_url: link.icon_url,
        }

        System.links.push(newLink);
        emplacement.links.push(newLink);
    }
</script>

<div>
    <button on:click={() => {System.pages.change("FolderEdit")}}>Annuler</button>
    <br/>
    <svelte:component this={Tree} {System} Stockage={System.folders[0]} move={copy} tab={0} />
</div>

<style>
    div {
        text-align:left;
    }
</style>