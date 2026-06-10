# Extracting `usmap` 

Most UE5 games use Unreal Engine's **IoStore** packaging format, which requires a `.usmap` file for modding tools to resolve asset names and without one you cannot unpack, browse, or modify any game content.

> [!NOTE]  
> If your game has `.ucas` and `.utoc` files in its Paks folder, it uses IoStore and you will need a `.usmap` file before you can unpack, inspect, or mod any assets.

There are three main tools that can generate one, each with different requirements:
- [UE4SS](https://github.com/UE4SS-RE/RE-UE4SS) - The easiest option, assuming it already runs on your game.
- [Dumper7](https://github.com/Encryqed/Dumper-7) - Most thorough option but requires compliing from source and DLL injection into the game process. ![new](https://img.shields.io/badge/←-BEST-brightgreen)   
- [JMap](https://github.com/trumank/jmap) - Standalone alternative with no requirements (but may fail).

<hr>

## Method: UE4SS

> [!NOTE]  
> You can skip to step 5 if you already have a working UE4SS for your game.

1. Navigate to [UE4SS-RE](https://github.com/UE4SS-RE/RE-UE4SS/releases/tag/experimental-latest) and download the latest version.
2. Extract the downloaded files into the bin directory, (Binaries\Win64) next to the game executable.
3. Open the `UE4SS-settings.ini` file in a text editor (e.g., Notepad++ or VSCode) and apply the Engine Version in the EngineVersionOverride section:

![UE4SS-settings.ini file open in editor showing EngineVersionOverride section with MajorVersion and MinorVersion fields set](/Media/UHT/1.png)

*(Match with your game's UE version, eg. UE5.7 -> Major:5, Minor: 7)*

4. In the Debug section make sure you enable `ConsoleEnabled`, `GuiConsoleEnabled`, and `GuiConsoleVisible`:

![UE4SS-settings.ini Debug section with ConsoleEnabled = 1, GuiConsoleEnabled = 1, and GuiConsoleVisible = 1 highlighted](/Media/UHT/2.png)

> [!IMPORTANT]  
> Some games may not work with UE4SS out of the box and will require additional configuration.

5. Launch the game and use the "Dumpers" tab of the UE4SS Debugging Tool to output the `.usmap` file.

![UE4SS debug tool GUI showing the Dumper tab selected with the Dump Mappings / usmap button visible and ready to click](/Media/Extractmappings/2.png)

6. The file will be output to: `...\Binaries\Win64\Mappings.usmap`

<br>
<hr>

## Method: Dumper7
Dumper7 is a powerful SDK and mapping dumper but requires compiling the tool from source before use. And requires an additional tool to inject the dll, which could be [CheatEngine](https://www.cheatengine.org/) or even [UUU](https://framedsc.com/GeneralGuides/universal_ue4_consoleunlocker.htm) (by changing the used dll)

1. Clone the [Dumper7 repository](https://github.com/Encryqed/Dumper-7), open the solution in Visual Studio and build the solution to get the dll.
2. Open CheatEngine and select the game process.

![Selecting the game process in CheatEngine ](/Media/Extractmappings/ce_1.png)

3. Inject DLL by going to Memory View -> Tools -> Inject DLL and selecting the Dumper7 dll.

![Injecting dll via CheatEngine's Memory View panel options](/Media/Extractmappings/ce_2.png)

4. Once the SDK generation is done, the mapping file can be found in:<br>
`C:\Dumper-7\<UE_Version>-<GameName>\Mappings`

![Generated Mapping file inside Dumper7 folder](/Media/Extractmappings/ce_3.png)

<br>
<hr>

## Method: JMap

1. Navigate to [jmap releases](https://github.com/trumank/jmap/releases/latest), download the latest release, and extract it.
2. Open CMD and `cd` to that folder (`cd "<folder_path>"`).
3. Set the UE version by executing the following: <br>
`set PATTERNSLEUTH_RES_EngineVersion=5.7` 
4. Open TaskManager, find your game's process, and copy the `PID`.
5. Execute the following to run jmap on the game:<br>
`jmap_dumper.exe --pid <PID> mappings.usmap`
6. Generated map will be created within the same folder as jmap.

![Using JMap via CMD commands](/Media/Extractmappings/jmap1.png)