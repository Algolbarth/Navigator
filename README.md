# Navigator

I re-create a file system based on Linux in order to manage my favorites.
Navigator was made with Svelte.

Navigator can add new links (with an url adress), edit it, move it in folders or copy it.

When you create a link, precise the url and the name you want to give for this link.
Same thing for folders, just give the name (folders don't have url they just contain links and other folders).

A new link or folder is created in the current folder.
If you don't have created folders, new files are stocked in root.

When you move a link Navigator just change the folder where is it.
When you move a folder, all its files move too.
Delete a folder delete all these files too (pay attention to not delete a folder if you want to keep files in it).

Links check automatically the icon file website and display it, but you can choose yourself the icon you want. Just put the new icon url in edit page.
Folders have a default icon but you can personalise them too.

Your links and folders are saved in your account file. This file is a .txt which countain all informations.
You can save it with the save option in menu.
At creation of your account, this file is automatically created.
Navigator warn you if you want to disconnect although some modifications are not saved since the last save action.
Attention : If you close Navigator less save, you will loose all modifications.
Finally, I recommend you to duplicate this account file. So you will have a chance to backup all your favorites if you save a bad modification.
