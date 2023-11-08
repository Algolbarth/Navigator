<script>
    import Tree from "./Tree.svelte";
    export let System;
    System;
    
    export function copy (folder) {
        copyFolder(System.edit, folder);
        System.pages.change("Menu");
    };

    function copyFolder (folder, emplacement) {
        let newFolder = {
            name: folder.name,
            icon: folder.icon,
            icon_url: folder.icon_url,
            links : [],
            folders : [],
        }

        for (let i = 0;i < folder.folders.length;i++) {
            copyFolder(folder.folders[i], newFolder);
        }
        for (let i = 0;i < folder.links.length;i++) {
            copyLink(folder.links[i], newFolder);
        }

        System.folders.push(newFolder);
        emplacement.folders.push(newFolder);
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