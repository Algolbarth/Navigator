<script>
    export let System;
    System;

    let name;
    let url;
    let icon = false;
    let icon_url = undefined;
    
    function addLink  () {
        if (System.checkInput(name) && System.checkInput(url) && (!icon || System.checkInput(icon_url))) {
            let link = {
                name: name,
                url: url,
                icon: icon,
                icon_url: icon_url,
            }
            if (!icon) {link.icon_url = undefined};
            System.links.push(link);
            System.currentFolder.links.push(link);
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
    <button class="validate" on:click={() => {addLink()}}>Ajouter</button>
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