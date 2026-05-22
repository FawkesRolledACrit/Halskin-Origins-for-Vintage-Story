# dnSpy Guide for Finding Character Creation Dialog

## Step-by-Step Instructions

### Step 1: Open dnSpy and Load the DLL

1. Open dnSpy
2. Click **File > Open...**
3. Navigate to your Vintage Story installation folder
4. Typical location: `C:\Program Files (x86)\Steam\steamapps\common\VintageStory\`
5. Select **VintagestoryLib.dll** and click Open

### Step 2: Search for the Character Creation Dialog

1. In dnSpy, press **Ctrl+Shift+K** (or click the magnifying glass icon in the left sidebar)
2. In the search box, type: `GuiDialog`
3. Click **Search** or press Enter
4. You'll see a list of all classes that contain "GuiDialog" in their name

### Step 3: Look for Character-Related Dialogs

Look through the list for classes with names like:
- `GuiDialogCharacterCreation`
- `GuiDialogCharacterSelect`
- `GuiDialogPlayerCharacter`
- `GuiDialogNewCharacter`
- `GuiDialogCreateCharacter`

**The most likely name is `GuiDialogCharacterCreation` or similar.**

### Step 4: Examine the Dialog Class

Once you find a likely candidate:

1. **Double-click** on the class name to open it
2. Look at the **namespace** at the top (e.g., `Vintagestory.GameContent` or `Vintagestory.Client`)
3. Look at the **methods** listed in the class

### Step 5: Find Key Methods

Look for methods with names like:
- `PopulateClasses` or `LoadClasses` - loads the class selection
- `OnClassSelected` or `OnClassChange` - handles when a class is selected
- `PopulateSkinParts` or `LoadSkinParts` - loads skin color options
- `OnSkinPartSelected` - handles skin color selection
- `Compose` or `BuildDialog` - builds the UI
- `TryOpen` or `OnOpenDialog` - opens the dialog

### Step 6: Note the Information

For each relevant method, note:
1. **Full class name** with namespace (e.g., `Vintagestory.GameContent.GuiDialogCharacterCreation`)
2. **Method name** (e.g., `PopulateClasses`)
3. **Method parameters** (what arguments it takes)
4. **Return type** (what it returns)

### Step 7: Share the Information

Tell me:
1. The full class name you found
2. The method names that handle:
   - Class selection
   - Skin color selection
   - UI composition

I'll then write the Harmony patches for you.

---

## Alternative: Search by String

If the above doesn't work, try searching for strings:

1. Press **Ctrl+Shift+F** in dnSpy
2. Search for: `characterClass`
3. This will find all code that references character classes
4. Look at the methods that use this string

---

## What You're Looking For (Examples)

You should find something that looks like this:

```csharp
namespace Vintagestory.GameContent
{
    public class GuiDialogCharacterCreation : GuiDialog
    {
        private List<string> availableClasses;
        private string selectedClass;
        
        public void PopulateClasses()
        {
            // Code that loads classes from characterclasses.json
        }
        
        public void OnClassSelected(string classCode)
        {
            // Code that handles class selection
        }
        
        public void PopulateSkinParts()
        {
            // Code that loads skin options
        }
    }
}
```

---

## Common Namespaces to Check

- `Vintagestory.GameContent` - most game content dialogs
- `Vintagestory.Client` - client-side dialogs
- `Vintagestory.Server` - server-side (unlikely for character creation)

---

## If You Get Stuck

1. Take a screenshot of dnSpy showing the class list
2. Or copy the class names you see
3. Share them with me and I'll help identify the right one
