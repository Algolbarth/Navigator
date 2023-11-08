<script>
    export let System;
    System;

    let name;

    function register () {
        if (System.checkInput(name)) {
            System.name = name;
            System.download(name + ".txt", name + "_");
            System.pages.change("Menu");
        }
    }
</script>

<h1>Navigator</h1>
<br/><br/>
Nom de compte
<br/>
<input bind:value={name} />
<br/><br/>
<button class="validate" on:click={register}>S'inscrire</button>
<br/><br/><br/>
<button on:click={() => {System.pages.change("Login")}}>J'ai déjà un compte</button>