<script>
    export let System;
    System;

    let files;
    let save;
    let step;

    async function login () {
        save = await files[0].text();
        step = 0;
        System.name = readValue();
        readFolder();
        System.currentFolder = System.folders[0];
        System.path.push(System.folders[0]);
        System.pages.change("Menu");
    }

    function readFolder () {
        let folder = {};
        folder.name = readValue();
        if (readValue() == "true") { folder.icon = true } else { folder.icon = false };
        folder.icon_url = readValue();
        folder.links = [];
        folder.folders = [];
        System.folders.push(folder);

        let folders = parseInt(readValue());
        for (let i=0;i<folders;i++) {
            let f = readFolder();
            folder.folders.push(f);
        }

        let links = parseInt(readValue());
        for (let i=0;i<links;i++) {
            let link = {};
            link.name = readValue();
            link.url = readValue();
            if (readValue() == "true") { link.icon = true } else { link.icon = false };
            link.icon_url = readValue();
            System.links.push(link);
            folder.links.push(link);
        }

        return folder;
    }

    function readValue() {
        let value = "";
        while (save[step] != "_" && step < save.length) {
            value += save[step];
            step++;
        }
        step++;
        return value;
    }

    /*
    fetch("test.txt")
    .then(response => response.text())
    .then((response) => {
        console.log(response)
    })
    .catch(err => console.log(err))
    */
</script>

<h1>Navigator</h1>
<br/><br/>
Fichier de sauvegarde
<br/> 
<input bind:files type="file" />
<br/><br/>
<button class="validate" on:click={login}>Se connecter</button>
<br/><br/><br/>
<button on:click={() => {System.pages.change("Register")}}>Créer un compte</button>