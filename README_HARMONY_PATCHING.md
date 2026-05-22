# Origins Mod - Harmony Patching Instructions

## Current Status

The JSON-only portion of the mod is complete and working:
- ✅ Character classes display with correct names and descriptions
- ✅ Traits display with correct names and descriptions
- ✅ Custom skin variants are available as additional options

## Remaining Tasks (Requires C# Harmony Patching)

To complete the mod's goals, we need to use Harmony to patch the character creation UI:

1. **Remove skin color selection** - Make it automatic based on selected origin
2. **Remove base classes** - Only show the 6 custom Origins
3. **Rename "Class" tab to "Origin"** - UI text change

## How to Find the Character Creation Dialog Class

### Step 1: Download dnSpy
- Download dnSpy from: https://github.com/dnSpy/dnSpy/releases
- It's a .NET decompiler and debugger

### Step 2: Open VintagestoryLib.dll
- Locate `VintagestoryLib.dll` in your Vintage Story installation directory
- Typical path: `C:\Program Files (x86)\Steam\steamapps\common\VintageStory\VintagestoryLib.dll`
- Open this file in dnSpy

### Step 3: Search for Character Creation Dialog
- In dnSpy, use Ctrl+Shift+K to search for types
- Search for terms like:
  - "Character"
  - "Creation"
  - "Dialog"
  - "GuiDialog"
- Look for classes in namespaces like:
  - `Vintagestory.GameContent`
  - `Vintagestory.Client`

### Step 4: Identify the Correct Class
- Look for methods related to:
  - Class selection
  - Skin color selection
  - Character creation UI composition
- The class likely extends `GuiDialog` or similar base class
- Note the full class name and namespace (e.g., `Vintagestory.GameContent.GuiDialogCharacterCreation`)

### Step 5: Find Methods to Patch
- Look for methods that:
  - Populate the class selection list
  - Handle class selection changes
  - Populate skin color options
  - Handle skin color selection
  - Compose the UI (likely named `Compose` or similar)
- Note the method names and their signatures

## Example Harmony Patch Structure

Once you find the correct class and methods, update `OriginsMod.cs` with the actual class names:

```csharp
[HarmonyPatch(typeof(Vintagestory.GameContent.GuiDialogCharacterCreation), "PopulateClasses")]
public class PopulateClassesPatch
{
    static bool Prefix(ref List<string> ___availableClasses)
    {
        // Filter to only show our origins
        ___availableClasses = new List<string>
        {
            "gloamish",
            "ascalen",
            "sailen",
            "virelian",
            "roven",
            "mireborn"
        };
        return false; // Skip original method
    }
}

[HarmonyPatch(typeof(Vintagestory.GameContent.GuiDialogCharacterCreation), "OnClassSelected")]
public class OnClassSelectedPatch
{
    static void Postfix(string selectedClass, ICoreClientAPI capi)
    {
        // Automatically set skin color based on origin
        SetSkinColorForOrigin(capi, selectedClass);
    }
}
```

## Building the C# Mod

### Prerequisites
- Visual Studio 2019 or later (Community Edition is free)
- .NET 6.0 SDK

### Build Steps
1. Open `OriginsMod.csproj` in Visual Studio
2. Update the reference paths to point to your actual Vintage Story installation
3. Build the project (Ctrl+Shift+B)
4. The compiled DLL will be copied to the mod folder automatically

## Alternative: Use dnSpy to Directly Patch

If you prefer not to set up a full C# development environment:

1. Open `VintagestoryLib.dll` in dnSpy
2. Navigate to the character creation dialog class
3. Right-click the method you want to patch
4. Select "Edit Method (C#)"
5. Make your modifications
6. Save the modified DLL (File > Save Module)
7. Replace the original `VintagestoryLib.dll` with your modified version

**Warning**: This modifies the game files directly and will be overwritten when the game updates. The Harmony approach is preferred for mod distribution.

## Next Steps

1. Use dnSpy to find the character creation dialog class
2. Identify the methods that handle:
   - Class population
   - Class selection
   - Skin color population
   - Skin color selection
   - UI composition
3. Update `OriginsMod.cs` with the correct class and method names
4. Build and test the mod

## Resources

- [Vintage Story Harmony Patching Wiki](https://wiki.vintagestory.at/Modding:Monkey_patching)
- [Harmony Documentation](https://harmony.pardeike.net/)
- [Vintage Story API Docs](https://apidocs.vintagestory.at/)
