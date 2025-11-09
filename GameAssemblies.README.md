# City of Gangsters - Game Assemblies

This package contains **publicized and stripped** game assemblies for **City of Gangsters** mod development using **BepInEx**.

## ⚠️ Important Notes

- These assemblies are **stripped and publicized** for modding purposes only
- They are **NOT** the original game files
- Use only for BepInEx mod development with City of Gangsters
- **Requires owning the original game**

## 📦 Installation

### For Mod Projects

Add to your `.csproj` file:

```xml
<PackageReference Include="MrPurple6411.CityOfGangsters.GameAssemblies" Version="1.4.4" PrivateAssets="all" />
```

### Via .NET CLI

```bash
dotnet add package MrPurple6411.CityOfGangsters.GameAssemblies
```

## 🛠️ Usage

This package automatically provides references to:

- `Assembly-CSharp.dll` - Main game logic
- `Assembly-CSharp-firstpass.dll` - Unity first-pass scripts
- `Unity.Timeline.dll` - Unity Timeline system
- `Unity.TextMeshPro.dll` - TextMeshPro support
- `Unity.Postprocessing.Runtime.dll` - Post-processing effects
- `Steamworks.NET.dll` - Steam integration

## 🔧 Development

All internal types are **publicized** for Harmony patching and modding access.

## 📄 Legal

These assemblies are processed derivatives for modding purposes. You must own the original City of Gangsters game to use this package.

## 🔗 Links

- [Source Repository](https://github.com/MrPurple6411/CityofGansters)
- [Game on Steam](https://store.steampowered.com/app/1386780/City_of_Gangsters/)
- [BepInEx Framework](https://github.com/BepInEx/BepInEx)