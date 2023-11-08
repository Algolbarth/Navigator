<script>
    export let System;
    System;

    let name = System.edit.name;
    let url = System.edit.url;
    let icon = System.edit.icon;
    let icon_url = System.edit.icon_url;
    
    function editLink () {
        if (System.checkInput(name) && System.checkInput(url) && (!icon || System.checkInput(icon_url))) {
            System.edit.name = name;
            System.edit.url = url;
            System.edit.icon = icon;
            if (icon) {
                System.edit.icon_url = icon_url;
            }
            else {
                System.edit.icon_url = undefined;
            }
            System.change = true;
            System.pages.change("Menu");
        }
	};

    function removeLink() {
        for (let i=0;i<System.links.length;i++) {
            if (System.links[i] == System.edit) {
                System.links.splice(i, 1);
            }
        }
        for (let i=0;i<System.currentFolder.links.length;i++) {
            if (System.currentFolder.links[i] == System.edit) {
                System.currentFolder.links.splice(i, 1);
            }
        }
        System.change = true;
        System.pages.change("Menu");
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
            URL : 
        </div>
        <div>
            <input bind:value={url}/>
        </div>
    </div>
    <div class="line">
        <div class="label">
            Icône :
        </div>
        <div>
            <button on:click={() => {icon = !icon}}>
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
    <button on:click={() => {System.pages.change("LinkCopy")}}>Copier</button>
    <button on:click={() => {System.pages.change("LinkMove")}}>Déplacer</button>
    <button class="cancel" on:click={() => {removeLink()}}>Supprimer</button>
    <button class="validate" on:click={() => {editLink()}}>Confirmer</button>
    <button on:click={() => {System.pages.change("Menu")}}>Annuler</button>
</div>

<style>
    .container {
        display:grid;
        grid-template-rows: 1fr 1fr;
        text-align:left;
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