<script>
    export let System;
    System;

    function editLink (link) {
        System.edit = link;
        System.pages.change("LinkEdit");
    }

    function editFolder (folder) {
        System.edit = folder;
        System.pages.change("FolderEdit");
    }

    function openFolder (folder) {
        System.currentFolder = folder;
        sort(System.currentFolder.folders);
        sort(System.currentFolder.links);
        System.path.push(folder);
        System.pages.change("Menu");
    }

    function returnFolder (index) {
        System.currentFolder = System.path[index];
        System.path.splice(index + 1, System.path.length - index);
        sort(System.currentFolder.folders);
        sort(System.currentFolder.links);
        System.pages.change("Menu");
    }

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
    }

    sort(System.currentFolder.folders);
    sort(System.currentFolder.links);

    $:save_state = (System.change) ? 'validate' : '';
</script>

<h1>Navigator</h1>
<br/><br/>
<button on:click={() => {System.pages.change("FolderAdd")}}>Créer dossier</button>
<button on:click={() => {System.pages.change("LinkAdd")}}>Créer raccourci</button>
<button on:click={() => {System.pages.change("Map")}}>Carte</button>
<button class={save_state} on:click={System.save}>Sauvegarder</button>
<button class="cancel" on:click={() => {System.pages.change("Logout")}}>Déconnecter</button>
<br/>
{#each System.path as folder, index}
    {#if index > 0}/{/if}<button class="link" on:click={() => {returnFolder(index)}}>{folder.name}</button>
{/each}
<br/>
{#if System.currentFolder != System.folders[0]}
    <div class="container">
        <div>
            <img src="Pictures/return.svg" alt="icon"/>
        </div>
        <div>
            <button class="link">..</button>
        </div>
        <div>
            <button class="link" on:click={() => {returnFolder(System.path.length - 2)}}>Retour</button>
        </div>
    </div>
{/if}
{#each System.currentFolder.folders as folder, index}
    <div class="container">
        <div>
            {#if folder.icon}
                <img src="{folder.icon_url}" alt="icon"/>
            {:else}
                <img src="Pictures/folder.svg" alt="icon"/>
            {/if}
        </div>
        <div>
            <button class="link" on:click={() => {editFolder(folder)}}>{folder.name}</button>
        </div>
        <div>
            <button class="link" on:click={() => {openFolder(folder)}}>Ouvrir</button>
        </div>
    </div>
{/each}
{#each System.currentFolder.links as link, index}
    <div class="container">
        <div>
            {#if link.icon}
                <img src="{link.icon_url}" alt="icon"/>
            {:else}
                <img src="https://s2.googleusercontent.com/s2/favicons?domain_url={link.url}" alt="icon"/>
            {/if}
        </div>
        <div>
            <button class="link" on:click={() => {editLink(link)}}>{link.name}</button>
        </div>
        <div>
            <a target="_blank" href="{link.url}">{link.url}</a>
        </div>
    </div>
{/each}

<style>
    .container {
        display:grid;
        width:100%;
        grid-template-columns: 0.15fr 1fr 4fr;
        text-align:left;
    }

    .container:hover {
        background:rgb(224, 224, 224);
    }

    .link {
        border:none;
        background:none;
        margin:0;
        padding:0;
        font-weight: bold;
        text-align:left;
    }

    .link:hover {
        color: green;
    }

    img {
        width:1.5vw;
    }

    .name {
        text-align:left;
    }
</style>