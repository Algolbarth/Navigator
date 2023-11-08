<script>
    export let System;
    System;

    if (!System.change) {logout()};

    function logout () {
        System.name = "";
        System.links = [];
        System.folders = [];
        System.currentFolder = {};
        System.path = [];
        System.edit = {};
        System.change = false;
        System.pages.change("Login");
    }
</script>

Attention vous avez des changements non sauvegardés !
<br/><br/>
<button class="cancel" on:click={logout}>Se déconnecter quand même</button>
<br/>
<button class="validate" on:click={() => {System.save();logout()}}>Sauvegarder puis se déconnecter</button>