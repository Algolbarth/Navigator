<script>
	export const System = {
		pages : {
			actual : {},
			list : [],
			add : function (name, svelte) {
				System.pages.list.push({
					name: name,
					svelte: svelte,
				});
			},
			getByName : function (name) {
				for (const page of System.pages.list) {
					if (page.name == name) {
						return page;
					}
				}
			},
			change : function (name) {
				System.pages.actual = System.pages.getByName(name);
			},
		},
		name: "",
		links: [],
		folders: [],
		currentFolder : {},
		path : [],
		change: false,
		edit: {},
		download: function (nom, text) {
			var element = document.createElement('a');
			element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(text));
			element.setAttribute('download', nom);
			element.style.display = 'none';
			document.body.appendChild(element);
			element.click();
			document.body.removeChild(element);
		},
		save: function () {
			let text = "";
			text += System.name + "_";
			text += System.saveFolder(System.folders[0]);
			System.download(System.name + ".txt", text);
			System.change = false;
		},
		saveFolder : function (folder) {
			let text = "";
			text += folder.name + "_" + folder.icon + "_" + folder.icon_url + "_";
			text += folder.folders.length + "_";
			for (const f of folder.folders) {
				text += System.saveFolder(f);
			}
			text += folder.links.length + "_";
			for (const link of folder.links) {
				text += link.name + "_" + link.url + "_" + link.icon + "_" + link.icon_url + "_";
			}
			return text;
		},
		checkInput: function (input) {
			if ([undefined, "", " "].includes(input)) {
				return false;
			}
			return true;
		},
	}

	import Menu from "./Menu.svelte";
	System.pages.add("Menu", Menu);

	import Map from "./Map.svelte";
	System.pages.add("Map", Map);

	import Login from "./Login.svelte";
	System.pages.add("Login", Login);

	import Register from "./Register.svelte";
	System.pages.add("Register", Register);

	import Logout from "./Logout.svelte";
	System.pages.add("Logout", Logout);

	import LinkAdd from "./LinkAdd.svelte";
	System.pages.add("LinkAdd", LinkAdd);

	import LinkEdit from "./LinkEdit.svelte";
	System.pages.add("LinkEdit", LinkEdit);

	import LinkMove from "./LinkMove.svelte";
	System.pages.add("LinkMove", LinkMove);

	import LinkCopy from "./LinkCopy.svelte";
	System.pages.add("LinkCopy", LinkCopy);

	import FolderAdd from "./FolderAdd.svelte";
	System.pages.add("FolderAdd", FolderAdd);

	import FolderEdit from "./FolderEdit.svelte";
	System.pages.add("FolderEdit", FolderEdit);

	import FolderMove from "./FolderMove.svelte";
	System.pages.add("FolderMove", FolderMove);

	import FolderCopy from "./FolderCopy.svelte";
	System.pages.add("FolderCopy", FolderCopy);

	System.pages.change("Login");
</script>

<div id="html">
	<div id="body">
		<svelte:component this={System.pages.actual.svelte} {System} />
	</div>
</div>

<style>
	#html {
		width:100vw;
		height:100vh;
	}

	#body {
		text-align:center;
		padding:1%;
	}

	:global(.validate) {
        background:rgb(0, 200, 0);
    }

    :global(.validate:hover) {
        background:rgb(0, 175, 0);
    }

	:global(.cancel) {
        background:rgb(200, 0, 0);
    }

    :global(.cancel:hover) {
        background:rgb(175, 0, 0);
    }
</style>