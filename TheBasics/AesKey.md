# Finding AES Key
Some games will have their `.pak` files encrypted with an AES key. </br>
Luckily, it's an easy task to find the AES key.

There are two methods:
- Method 1: using [AESDumpster](https://github.com/GHFear/AESDumpster) by [GHFear](https://github.com/GHFear/)
- Method 2: using the Java version Aes_Finder (backup if first doesn't work).

## Getting the AES - Method 1
1. Navigate to [AESDumpster](https://illusory.dev/aesdumpster/) (web-based & fast).
2. Drag and drop the game's binary exe into the website (usually called "GameName-Win64-Shipping.exe").
3. Within a few seconds, it will output the found AES key on the screen (if any).

## Getting the AES - Method 2
1. Download the [AES_Finder.exe](https://github.com/Dmgvol/UE_Modding/raw/main/Tools/AES_finder.exe).<br>
_(the tool is using Java, and requires Java Runtime to be installed)_
2. Place the `.exe` in the same folder as the game binary executable.<br>
_(the one with "Win64-Shipping.exe" in its name)_<br>
(For example: `...\Ghostrunner 2\Ghostrunner2\Binaries\Win64\`)
3. Launch the game and then launch the AES finder.
4. Wait a few seconds, and a new text file named `key.txt` will appear in that folder, which will contain the AES key.

That's it!
