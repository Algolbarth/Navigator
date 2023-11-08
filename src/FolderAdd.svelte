<script>
    export let System;
    System;

    let name;
    let icon = false;
    let icon_url = undefined;
    
    function addFile  () {
        if (System.checkInput(name) && (!icon || System.checkInput(icon_url))) {
            let folder = {
                name: name,
                icon: icon,
                icon_url: icon_url,
                links : [],
                folders : [],
            }
            if (!icon) {folder.url = undefined};
            System.folders.push(folder);
            System.currentFolder.folders.push(folder);
            System.change = true;
            System.pages.change("Menu");
        }
	};
</script>

<div class="container">
    <div class="line">
        <div class="label">
            Titre : 
        </div>
        <div>
            <input bind:value={name}/>
        </div>
    </div>
    <div class="line">
        <div class="label">
            Icône : 
        </div>
        <div>
            <button on:click={() => {icon=!icon}}>
                {#if icon}
                    Personalisée
                {:else}
                    Par défaut
                {/if}
            </button>
        </div>
    </div>
    {#if icon}
        <div class="line">
            <div class="label">
                URL de l'icône : 
            </div>
            <div>
                <input bind:value={icon_url}/>
            </div>
        </div>
    {/if}
</div>

<div style="text-align:right;">
    <button class="validate" on:click={() => {addFile()}}>Ajouter</button>
    <button on:click={() => {System.pages.change("Menu")}}>Annuler</button>
</div>

<style>
    .container {
        display:grid;
        grid-template-rows: 1fr 1fr;
        text-align: left;
    }

    .line {
        display:grid;
        grid-template-columns: 1fr 5fr;
    }

    .label {
        text-align:right;
        margin:10px;
    }

    input {
        width:100%;
    }
</style>