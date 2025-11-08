# Modernized City of Gangsters Modding Workspace

A professional BepInEx modding workspace for City of Gangsters with automated build system, hybrid git tag versioning, and GitHub Actions CI/CD.

## 🚀 Quick Start

### Prerequisites
- .NET 8.0 SDK
- City of Gangsters (Steam)
- BepInEx 5.4.22+ installed in game directory

### First-Time Setup

1. **Process game assemblies** (required before building mods):
   ```powershell
   .\scripts\Process-Assemblies.ps1 1.4.4
   # OR with auto-publish (commits, tags, and triggers CI/CD):
   .\scripts\Process-Assemblies.ps1 1.4.4 -AutoPublish
   ```

2. **Build the example mod**:
   ```bash
   dotnet build src/ExampleMod/ExampleMod.csproj -c Debug
   ```

3. **Test in game** - The mod DLL is auto-copied to your BepInEx plugins folder!

## Project Structure

```
├── .github/workflows/          # GitHub Actions workflows
├── build/                      # MSBuild configuration
│   ├── Common.props           # Common project properties
│   └── BepInEx.targets        # BepInEx-specific build targets
├── src/                       # Your mod projects go here
├── Docs/                      # Documentation
├── CityofGangstersDecompiled/ # Decompiled game source (reference)
├── Directory.Build.props      # Global MSBuild properties
└── Directory.Build.targets    # Global MSBuild targets
```

## Creating a Mod

### 1. Project Template

Create a new mod project in the `src/` directory:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  
  <PropertyGroup>
    <AssemblyTitle>My Awesome Mod</AssemblyTitle>
    <AssemblyDescription>Makes the game more awesome</AssemblyDescription>
    <AssemblyVersion>1.0.0.0</AssemblyVersion>
  </PropertyGroup>
  
  <!-- BepInEx Plugin Metadata -->
  <ItemGroup>
    <BepInPlugin Include="com.mrpurple6411.myawesomemod" />
    <BepInPlugin Include="My Awesome Mod" />
    <BepInPlugin Include="1.0.0" />
  </ItemGroup>
  
</Project>
```

### 2. Basic Plugin Code

```csharp
using BepInEx;
using HarmonyLib;

namespace MyAwesomeMod
{
    [BepInPlugin("com.mrpurple6411.myawesomemod", "My Awesome Mod", "1.0.0")]
    public class Plugin : BaseUnityPlugin
    {
        private void Awake()
        {
            var harmony = new Harmony("com.mrpurple6411.myawesomemod");
            harmony.PatchAll();
            
            Logger.LogInfo("My Awesome Mod loaded!");
        }
    }
}
```

## Build Configurations

### Local Development

For local development with automatic copying to BepInEx plugins folder:

```bash
dotnet build -c Debug
```

This will:
- Build your mod
- Copy DLL and PDB files to `BepInEx/plugins/`
- Enable debugging with Visual Studio/VS Code

### Release Build

For distribution:

```bash
dotnet build -c Release
```

This will:
- Build optimized release version
- Create a distributable ZIP package
- Generate NuGet package (if configured)

## MSBuild Features

### Automatic Game Detection

The build system automatically detects your City of Gangsters installation:

1. `C:\Program Files (x86)\Steam\steamapps\common\City of Gangsters`
2. `C:\Program Files\Steam\steamapps\common\City of Gangsters`  
3. `GameDir` environment variable
4. `GameDir` MSBuild property

### Custom MSBuild Targets

- **`StartGame`** - Launch the game for testing
- **`PublicizeAssemblies`** - Create publicized versions of game assemblies
- **`CreateModPackage`** - Create distributable mod package

```bash
dotnet build -t:StartGame        # Launch the game
dotnet build -t:PublicizeAssemblies  # Publicize game assemblies
```

## GitHub Actions

### Automated Builds

Every push triggers:
- Multi-configuration builds (Debug/Release)
- Automated testing
- Artifact generation
- NuGet package creation

### Assembly Publicization

The processing script uses **BepInEx.AssemblyPublicizer.Cli** to:
- **Publicize internal APIs** - Makes internal types/members accessible for Harmony patching
- **Strip assemblies** - Removes unnecessary code while keeping runtime safety  
- **Prevent duplicates** - Smart checking against existing tags and hashes
- **Auto-publish** - Optional automated git workflow

Only the core game assemblies are processed:
- `Assembly-CSharp.dll` - Main game logic
- `Assembly-CSharp-firstpass.dll` - First-pass scripts

### Release Automation

On GitHub releases:
- Build all mods
- Create distribution packages
- Publish to NuGet
- Attach assets to release

## NuGet Packages

### Game Assemblies Package

Publicized game assemblies are packaged as:
```
MrPurple6411.CityOfGangsters.GameAssemblies
```

This enables:
- CI/CD builds without game files
- Version-controlled dependencies
- Easy sharing between developers

### Using in Your Mods

The build system automatically references the NuGet package in CI environments and falls back to local assemblies for development:

```xml
<!-- Automatically handled by the build system -->
<PackageReference Include="MrPurple6411.CityOfGangsters.GameAssemblies" Version="1.0.0" PrivateAssets="all" Condition="'$(UseLocalGameAssemblies)' != 'true'" />
```

## Processing Game Assemblies

When the game updates, process assemblies locally with duplicate prevention:

```powershell
# Process new game version - automatically detects changes
.\scripts\Process-Assemblies.ps1 1.4.4

# Auto-publish if assemblies changed (commits, tags, triggers CI/CD)
.\scripts\Process-Assemblies.ps1 1.4.4 -AutoPublish

# Force reprocess even if no changes detected
.\scripts\Process-Assemblies.ps1 1.4.4 -Force
```

### Smart Duplicate Prevention

The script prevents unnecessary work by:
- **Checking GitHub tags** - Skips if `assemblies-v1.4.4` already published
- **Hash tracking** - Compares processed assemblies against previous runs
- **Auto-publish** - Only commits/tags if assemblies actually changed

### Output

Processed assemblies go to:
- `lib/net48/` - Publicized and stripped game assemblies
- `assembly-hashes.json` - Hash tracking for duplicate prevention

Unity dependencies are **not included** - use official Unity NuGet packages instead.

## Configuration

### Environment Variables

- `GAME_DIR` - Override game installation path
- `USE_LOCAL_ASSEMBLIES` - Force use of local game files instead of NuGet

### MSBuild Properties

- `GameDir` - Game installation directory
- `UseLocalGameAssemblies` - Use local game files (true/false)
- `PublicizeGameAssemblies` - Enable assembly publicization

## Debugging

### Visual Studio Setup

1. Set your mod project as startup project
2. In project properties, set:
   - **Start external program**: `$(GameDir)\City of Gangsters.exe`
   - **Working directory**: `$(GameDir)`
3. Build in Debug mode
4. Press F5 to start debugging

### VS Code Setup

Use the provided launch configuration in `.vscode/launch.json`:

```json
{
  "name": "Debug Mod",
  "type": "coreclr",
  "request": "launch",
  "program": "${workspaceFolder}/GameDir/City of Gangsters.exe",
  "cwd": "${workspaceFolder}/GameDir",
  "stopAtEntry": false
}
```

## Contributing

1. Fork the repository
2. Create your mod in `src/YourModName/`
3. Follow the coding standards
4. Submit a pull request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- **BepInEx Team** - For the excellent modding framework
- **Harmony** - For runtime patching capabilities  
- **SomaSim** - For creating City of Gangsters
- **Community** - For mod ideas and testing

---

For detailed game analysis and modding insights, see [Game Analysis](Docs/GameAnalysis.md).