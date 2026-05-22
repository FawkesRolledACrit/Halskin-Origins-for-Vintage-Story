# Build Instructions

## Prerequisites
- .NET 6.0 SDK (download from https://dotnet.microsoft.com/download)

## Build Steps

1. Open Command Prompt or PowerShell
2. Navigate to the OriginsMod folder:
   ```
   cd C:\Users\Fawke\OriginsMod
   ```

3. Set the Vintage Story path environment variable:
   ```
   set VintageStoryPath=C:\Program Files (x86)\Steam\steamapps\common\VintageStory
   ```
   (Adjust this path if your Vintage Story is installed elsewhere)

4. Build the project:
   ```
   dotnet build
   ```

5. The compiled DLL will be copied to:
   ```
   C:\Users\Fawke\AppData\Roaming\VintageStoryData\Mods\origins\origins.dll
   ```

6. Restart Vintage Story

## Current Status

The Harmony patches are set up to:
- ✅ Filter character classes to only show the 6 Origins (via `PopulateClasses` patch)
- ⏳ Auto-set skin color based on selected origin (method needs verification)
- ⏳ Rename "Class" tab to "Origin" (method needs verification)

## Testing

After building and restarting Vintage Story:
1. Create a new world
2. Check if only the 6 Origins appear in the class selection
3. Check the logs for any Harmony patch errors

## If Build Fails

If you get errors about missing references, make sure:
1. The Vintage Story path is correct
2. Vintage Story is installed at that location
3. The files `0Harmony.dll` and `VintagestoryApi.dll` exist in the `Lib` folder
