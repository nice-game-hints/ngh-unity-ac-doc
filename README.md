First, install Adventure Creator following its instructions.

# Instructions on using this package
1. Install the package `com.nicegamehints.unity.ac` through the Package Manager
2. Create an empty GameObject that will control the hints
3. Attach the NGHMenu component to the GameObject
  - If you are creating a custom menu (not using AC.Menu), you should use
    a GameObject (for example Vertical Layout Group) that is under the Canvas, the component will append the guides
    under the GameObject it is attached to
4. Select the Mode from the NGHMenu Inspector
 - "Adventure Creator Menu" uses the menus from the AC Menu manager, supports also prefab menus
 - "Adventure Creator Generic" lets you create custom `UnityEngine.UI` based menus that do not use Adventure Creator menu manager
5. Adjust the script execution order
 1. Go to Edit > Project Settings > Script Execution Order
 2. Add NGHMenu to the list and load it _before_ Default time
6. Type the location of the NGH markdown files to the Hints Path (for example: Assets/ngh/)

## Instructions on using the Adventure Creator Menu mode
### The guide view
1. Attach the AC Menu Manager to the NGHMenu component
2. Create a menu in AC Menu manager. Name it NGHGuides and select "Unity Ui Prefab" as the source
3. Create the prefab menu scene and attach it to the NGHGuides menu
 - Linked Canvas prefab
4. Add something that will contain the guide buttons
 - For example, add a Canvas and set the size
 - Add a Vertical Layout Group into the Canvas GameObject
5. Add a sample GuideButton into the prefab canvas, preferably inside the Canvas above
 - This button defines what the buttons for the active guides will look. It is cloned for the guides.
6. Add the sample guide button (name: GuideButton) also into the NGHGuides menu
 - To the Linked button, drag the sample button from the prefab canvas
 - Select "Crossfade" for the Click type
 - Select Menu to switch to "NGHHints"

### The Hint view
1. Create a menu in AC Menu manager. Name it NGHHints and select "Unity Ui Prefab" as the source
2. Add a label to the NGHHints menu, name it HintContent
3. Add a button to the NGHHints menu, name it NextHintButton
 - On Click type select Custom Script
4. Create the prefab menu scene and attach it to the NGHHints menu
 - Linked Canvas prefab
5. Add a text that will show the hint contents
 - Link this text to the label in the NGHHints menu
6. Add a button that will advance to the next hint
 - Link this button to the button in the NGHHints menu

### Note for non-prefab menu
If you do not use prefab and are using AC 1.79.2 or older, you have to tweak AC a little
1. Open Assets/AdventureCreator/Scripts/Menu/Menu.cs
2. On line 1598 (above the ResetVisibleElements) add `elementCount = -1;`
