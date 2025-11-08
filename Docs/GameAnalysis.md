# City of Gangsters - Decompiled Game Analysis

## Overview
This workspace contains the decompiled source code for **City of Gangsters**, a Unity-based strategy game, and serves as a **BepInEx modding workspace**. The repository is owned by MrPurple6411 and contains a complete decompilation of the game's C# assemblies and Unity engine modules for reference and mod development.

## Project Structure

### Root Directory Structure
```
c:\Repos\MrPurple6411\CityofGansters\
├── .git/                     # Git repository metadata
├── .gitignore               # Standard Visual Studio gitignore (excludes CityofGangstersDecompiled/)
└── CityofGangstersDecompiled/   # Main decompiled content
```

### Key Characteristics
- **Project Type**: Decompiled Unity game source code
- **Primary Language**: C# (.NET Framework)
- **Engine**: Unity (extensive module structure)
- **Steam Integration**: Uses Steamworks SDK
- **Architecture**: Service-oriented with modular design

## Core Game Structure

### Main Assemblies
1. **Assembly-CSharp** - Primary game logic
2. **Assembly-CSharp-firstpass** - First-pass compilation scripts
3. **Unity Engine Modules** - 60+ Unity engine modules
4. **External Libraries** - Third-party dependencies

### Game Architecture

#### Core Game Entry Point
- Main game class: `Game.Game` (MonoBehaviour)
- Initialization flow: Platform → Services → Session
- Uses coroutine-based initialization system

#### Service Architecture
The game uses a sophisticated service-oriented architecture:

```
ServiceContext serves as dependency injection container
├── Audio Services
├── Input Services  
├── Map Services
├── UI Services
├── Analytics Services
├── Discord Integration
├── Save/Load Services
└── Localization Services
```

### Key Game Systems

#### 1. Core Game Logic (`Game.Core/`)
- **Pathfinding System**: Advanced grid-based pathfinding
- **Spatial Systems**: 
  - Grid transforms and world positioning
  - Heat maps and territory control
  - Node-based world representation
- **Economic Systems**:
  - Money and pricing systems
  - Resource management
  - Crew statistics and management

#### 2. Services Layer (`Game.Services/`)
Major services include:
- **SaveLoadService**: Game state persistence
- **LocalizationService**: Multi-language support
- **UIService**: User interface management
- **CameraService**: Camera control and positioning
- **AnalyticsService**: Player behavior tracking
- **DiscordService**: Discord Rich Presence integration

#### 3. Session Management (`Game.Session/`)
- Game state management
- Player progression
- Campaign/scenario handling

### Technical Features

#### Unity Integration
- **Steam Integration**: Full Steamworks SDK implementation
- **Graphics**: Uses Unity's post-processing pipeline
- **UI**: Unity UI system with custom components
- **Audio**: Comprehensive audio service layer

#### Advanced Systems
- **Modding Support**: Dedicated modding infrastructure
- **Settings Management**: Comprehensive configuration system
- **Debug Tools**: SR Debugger integration
- **Analytics**: Player behavior and performance tracking

### Dependencies & External Libraries

#### Third-Party Components
- **Steamworks.NET**: Steam platform integration
- **StompyRobot.SRDebugger**: Runtime debugging tools
- **Unity Post-processing**: Visual effects pipeline
- **TextMeshPro**: Advanced text rendering

#### Custom Libraries
- **BotL**: Custom utility library
- **CatSAT**: Constraint satisfaction solver
- **Logger**: Custom logging framework

## Development Insights

### Code Quality Indicators
- **Service Pattern**: Well-architected dependency injection
- **Event System**: Comprehensive event bus implementation
- **Separation of Concerns**: Clear separation between game logic, UI, and platform code
- **Extensibility**: Modular design allows for easy extension

### Notable Features
- **Cross-platform Support**: Platform abstraction layer
- **Localization**: Full internationalization support
- **Save System**: Sophisticated serialization with concurrent save support
- **AI Systems**: Advanced AI advisor configurations
- **Territory Control**: Complex heat map and influence systems

## Technical Observations

### Strengths
- Well-organized service architecture
- Comprehensive Unity integration
- Strong separation between game logic and platform code
- Extensive configuration and settings management
- Professional-grade debugging and analytics integration

### Architecture Patterns
- **Service Locator Pattern**: ServiceContext as central registry
- **Observer Pattern**: Extensive event system
- **Strategy Pattern**: Platform-specific implementations
- **Factory Pattern**: Service creation and management

## Modding Target Areas

Based on the code analysis, here are key areas modders should examine for different types of modifications:

### **Economic/Resource Mods**
- **`Game.Core/`** - Money and pricing systems, resource management algorithms
- **`Game.Services/SaveLoadService`** - Game state persistence for economic data
- **Crew statistics and management** - Located in core game logic assemblies

### **AI/Behavior Mods** 
- **`BotL/`** - Logic programming engine for AI decision making
- **`Game.Services/`** - AI advisor configurations and behavior systems
- **`CatSAT/`** - Constraint satisfaction solver for AI planning

### **UI/Interface Mods**
- **`Game.Services/UIService`** - User interface management and state
- **Unity UI components** - Custom UI elements and controls
- **`Game.Services/LocalizationService`** - Text and language systems

### **Map/Territory Mods**
- **`Game.Core/`** - Spatial systems, grid transforms, world positioning
- **Heat maps and territory control** - Node-based world representation
- **Pathfinding system** - Advanced grid-based pathfinding algorithms

### **Save/Progression Mods**
- **`Game.Services/SaveLoadService`** - Sophisticated serialization system
- **`Game.Session/`** - Game state management, player progression, campaign handling
- **Concurrent save support** - Multi-threaded save operations

### **Analytics/Debug Mods**
- **`Game.Services/AnalyticsService`** - Player behavior tracking systems
- **`StompyRobot.SRDebugger`** - Runtime debugging infrastructure (if accessible)
- **Event system** - Comprehensive event bus for monitoring game state

### **Platform/Integration Mods**
- **`Game.Services/DiscordService`** - Discord Rich Presence integration
- **Platform abstraction layer** - Cross-platform support systems
- **Steam integration** - Achievement, cloud save, and platform features

## Conclusion

This appears to be a professionally developed strategy game with sophisticated systems for territory control, resource management, and player progression, built using modern Unity development practices. The decompiled code reveals a well-structured, maintainable codebase that demonstrates enterprise-level game development techniques.

The game's architecture shows clear separation of concerns with a robust service-oriented design, making it well-suited for modding through BepInEx and Harmony patching of the internal APIs.

---
*Analysis completed on November 8, 2025*