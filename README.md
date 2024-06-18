First, install Adventure Creator following its instructions.

# Instructions on using this package
1. Install the package `com.nicegamehints.unity.ac` through the Package Manager
2. Create an empty GameObject that will control the hints, name it "NGHHintController".
3. Attach the NGHMenu component to the GameObject
4. Select the Mode from the NGHMenu Inspector
    - "Adventure Creator Menu" uses the menus from the AC Menu manager, supports also prefab menus
    - "Adventure Creator Generic" lets you create custom `UnityEngine.UI` based menus that do not use Adventure Creator menu manager
5. Adjust the script execution order
    1. Go to Edit > Project Settings > Script Execution Order
    2. Add NGHMenu to the list and load it _before_ Default time
6. If you are using AC 1.79.x, change the "AC Assembly Name" to `Assembly-CSharp` under the Advanced

## Instructions on using the Adventure Creator Menu mode
In-game hints need two menu views: Guides view and Hints view.

In the Guides view are listed all the active guides at the moment. The user can click one of the guides to see hints regarding that guide.
In the Hints view the selected guide is shown as a series of gradual hints. There should be a "Next hint" button to navigate to the next hint in the guide.

First, Attach the AC Menu Manager to the NGHMenu component.
![AC Menu Manager attached to the NGHMEnu component ><](https://raw.githubusercontent.com/nice-game-hints/ngh-unity-ac-doc/main/NGHMenuComponent.png)

### The Guides view
1. Create a prefab menu Canvas. Name it "GuidesMenu". The Canvas should include at least the following UI items:
    - Another Canvas that has a Vertical Layout Group component
    - Inside that Canvas, a Button. This button will be the sample button that will be cloned when listing the active guides.
![Prefab Guide Menu with the vertical layout group ><](https://raw.githubusercontent.com/nice-game-hints/ngh-unity-ac-doc/main/GuideMenuWithVerticalLayout.png)
2. Create a menu in AC Menu manager. Name it "NGHGuides" and select "Unity Ui Prefab" as the source
3. Add a button named GuideButton inside the NGHGuides menu.
   - Click type is "Crossfade"
   - Menu to switch to: "NGHHints" (this will be created next)
4. Attach the prefab to the NGHGuides menu
    1. Drag the GuidesMenu prefab from Assets to Linked Canvas prefab
    2. Drag the button from the prefab to GuideButton Linked button
![Guides Menu in AC Menu Manager ><](https://raw.githubusercontent.com/nice-game-hints/ngh-unity-ac-doc/main/NGHGuidesMenu.png)

You should be now able to see the menu in the game. You still need to show the menu somehow. The easiest (for testing) is to have it "Enabled on start".

### The Hints view
1. Create a prefab Canvas. Name it "HintsMenu". The Canvas should include at least following UI items:
    - A text (legacy) element (as of Adventure Creator 1.79.2 you cannot link TMP text to a Menu Label?) that will show the text content of the hint.
    - A button (no need to be legacy) that will show the user the next hint. Will be automatically hidden when there are no more hints.
    - _Optional_: A text (legacy) showing the current guide title
    - _Optional_: A RawImage showing an image if the current hint has one
2. Create a menu in AC Menu Manager. Name it "NGHHints" and select "Unity Ui Prefab" as the source
3. Add a label named "HintContentText" inside the NGHHints menu
4. Add a button named "NextHintButton" inside the NGHHints menu
   - On Click type select Custom Script
5. Attach the prefab to the NGHGuides menu
    1. Drag the HintsMenu prefab from Assets to Linked Canvas prefab
    2. Drag the text from the prefab to HintContentText Linked Text
    3. Drag the button from the prefab to the NextHintButton Linked button
5. _Optional_: Add a label named "GuideTitle" inside the NGHHints menu
    - Drag the corresponding text from the prefab to the Linked Text
6. _Optional_: Add a graphic named "HintContentImage" inside the NGHHints menu
    - Select UI image type to "Raw Image"
    - Drag the corresponding raw image from the prefab to the Linked Raw Image
![Hints Menu in AC Menu Manager ><](https://raw.githubusercontent.com/nice-game-hints/ngh-unity-ac-doc/main/NGHHintsMenu.png)

You should be now able to click the guide button (set is visible in AC Menu Manager) in the Guides view and it should show you the HintsMenu prefab with default values.

You might want to implement close buttons to each menu but that is outside the scope of this guide.

## Attaching the actual hints to the NGHMenu
1. Create a folder named "ngh" inside Assets
2. Create a new file named "sample.md" inside the ngh folder
3. Add following content inside the sample.md file
```
---
title: A sample guide
---

#
This is the first hint

#
This is the second hint
```
4. In NGHMenu component, fill the Hints path with "Assets/ngh/"

If you now open the Guides view, you should see a button with the text "A sample guide". You might also see the default guide. You can set it non-visible in the AC Menu Manager.
When you click the "A sample guide" button you should see the Hints view. It will show you the text "This is the first hint". When you click the next hint button you should see the text "This is the second hint" and the next hint button becomes invisible.

### Creating a conditional guide
1. Create a new file named "conditional.md" inside the ngh folder. Please note the name can be anything but don't use spaces in the name.
2. Find two boolean variables from your game inside the Variable Manager. Take note of the name of the variables. Lets say they are "Variable 1" and "Variable 2".
4. Add the following content inside the conditional.md file
```
---
title: This guide is visible when variable one is true
when: Variable 1
---

# ((when Variable 2))
This hint is visible when variable two is true.

# ((until Variable 2))
This hint is visible when variable two is false.
```

If you now open the Guides view, you should see only the sample.md. Set the Variable 1 to true in the game and open the Guides menu, again. You should now see both sample.md and conditional.md guides. The hints of the conditional guide are shown depending on the
value of Variable 2.
