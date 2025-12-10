# DJI Waypoint KMZ Generator

A DJI drone waypoint planning tool based on Vue 3 + CesiumJS, supporting the generation of KMZ waypoint files compatible with WPML 1.0.6 standard. These files can be directly imported into DJI FlightHub 2 and Matrice series drones.

![License](https://img.shields.io/badge/license-GPL--3.0-blue.svg)
![Vue](https://img.shields.io/badge/Vue-3.5-brightgreen.svg)
![Cesium](https://img.shields.io/badge/Cesium-1.135-blue.svg)

[English](./README_EN.md) | [简体中文](./README.md)

> 📢 **Open Source Note**: This project will be officially open-sourced when it reaches **100 Stars**! Your **Star** is our motivation! 🚀

## ⭐ Star History

[![Star History Chart](https://api.star-history.com/svg?repos=hecongyuan/dji_way_line&type=Date)](https://star-history.com/#hecongyuan/dji_way_line&Date)

## 🎨 Interface Preview

### Main Interface
![Main Interface](doc/images/main_interface.png)
- Left: Control Panel (Mission Config, Waypoint List)
- Right: 3D Map View (Route Preview)
- Bottom: Coordinate Information

### Create Mission
![Create Mission](doc/images/create_mission.png)
- Currently supported route types: Patrol Route, Area Route (More types in development)
- Select aircraft model (Matrice 3/4 series)
- Select payload (Matrice 4E/4T)
- Custom mission name

### Feature Showcase

#### 1. Height Mode Visualization
![Height Mode](doc/images/height_mode.png)
Each height mode has a corresponding schematic:
- Absolute Height: Based on sea level
- Relative to Takeoff: Relative to the takeoff point
- Relative to Ground (Real-time Follow): Follows terrain undulations in real-time

#### 2. Climb Mode Settings
![Climb Mode](doc/images/climb_mode.png)
- Vertical Climb: Ascend vertically to safe altitude first, then fly to the first waypoint
- Diagonal Climb: Fly directly to the first waypoint diagonally

#### 3. AI Patrol Path Planning
![AI Patrol](doc/images/ai_patrol.png)
- Automatically generate S-shaped scanning paths
- Real-time preview of scanning coverage
- Adjustable scanning spacing and direction

## 📅 Roadmap

- ✅ **Patrol Route Generation & FlightHub 2 Compatibility**
- ✅ **Matrice 4T Real-world Testing**: Verified flight and photography functions in actual environments with Matrice 4T.
- [ ] **AI Patrol Integration**:
   - [ ] Real-time target recognition (Person, Vehicle, Boat, etc.).
   - [ ] Save recognition results (Images/Videos) to drone storage.

## ✨ Core Features

### 🗺️ Route Planning
- **Visual Map Editing**: 3D map interface based on AMap + CesiumJS
- **Currently Supported Route Types**:
  - **Patrol Route**: Add waypoints on map, support loop or one-way patrol missions
  - **Area Route**: Draw area to auto-generate S-shaped scanning paths with AI target recognition support
  - More route types (Waypoint, Linear, Oblique, Geometry, etc.) are in development
- **Real-time Preview**: Real-time display of route path, supporting closed loops and one-way routes
- **Coordinate Transformation**: Automatic conversion between GCJ-02 (AMap) and WGS84 (GPS) coordinate systems

### 🤖 Area Route AI Scan (Matrice 4T)
- **Smart Scan Path Generation**: Automatically generate S-shaped scanning paths
- **Target Recognition Config**: Support Person, Vehicle, and Boat target types
- **Adjustable Parameters**:
  - Scan Spacing (5-200m)
  - Route Direction (0-359°)
  - Boundary Margin (0-50m)
  - Gimbal Pitch (-90° ~ 30°)
- **Overlap Settings**: Heading overlap 80%, Side overlap 70%

### 📐 Height Modes
- **Absolute Height (WGS84)**: Absolute altitude based on WGS84 ellipsoid
- **Relative to Takeoff**: Height relative to the takeoff point
- **Relative to Ground (Real-time Follow)**: Real-time terrain following, maintaining constant height above ground

### 🎯 Mission Configuration
- **Flight Parameters**: Speed, Height, Takeoff Safe Altitude
- **Lost Control Action**: Go Home, Hover, Land, Continue
- **Finish Action**: Go Home, Land, Hover, Return to First Waypoint
- **Climb Mode**: Vertical Climb, Diagonal Climb

### 📦 KMZ Import/Export
- **Export KMZ**: Generate KMZ files compatible with WPML 1.0.6 standard
- **Import KMZ**: Parse existing KMZ files to restore route and configuration
- **Compatibility**: Fully compatible with DJI FlightHub 2 and Matrice series drones

## 🚀 Quick Start

### Requirements
- Node.js >= 20.x
- pnpm >= 10.x (Recommended) or npm

### Install Dependencies
```bash
# Using pnpm (Recommended)
pnpm install

# Or using npm
npm install
```

### Development
```bash
# Start development server
pnpm dev

# Or
npm run dev
```

Visit `http://localhost:5173` to use.

### Production Build
```bash
# Build for production
pnpm build

# Or
npm run build
```

Build artifacts will be output to the `dist` directory.

## 📖 User Guide

### 1. Draw Route

#### Patrol Route
1. Select "Patrol Route" type
2. Click on the map to add patrol waypoints
3. Configure waypoint parameters (speed, height, gimbal angle)
4. Support loop patrol and one-way patrol

#### Area Route (AI Scan)
1. Select "Area Route" type
2. Draw scan area on the map (at least 3 points)
3. System automatically generates S-shaped scanning path
4. Adjust scan parameters (spacing, direction, margin)
5. Select AI recognition targets (Person, Vehicle, Boat) - Matrice 4T only

### 2. Configure Parameters

#### Basic Parameters
- **Flight Speed**: 1-15 m/s, recommended 10 m/s
- **Flight Height**: 20-500 m, recommended 60 m
- **Takeoff Safe Altitude**: 10-200 m, recommended 20 m

#### Height Mode Selection
- **Absolute Height**: Suitable for flat terrain
- **Relative to Takeoff**: Suitable when takeoff point and target area have similar altitude
- **Relative to Ground**: Suitable for mountainous or hilly terrain with large undulations

### 3. Generate KMZ

1. Click **Generate KMZ** button
2. File automatically downloads (`mission.kmz`)
3. Import into DJI FlightHub 2 or drone remote controller

### 4. Import KMZ

1. Click **Import KMZ** button
2. Select existing KMZ file
3. System automatically parses and restores route and configuration

## 🛠️ Tech Stack

### Frontend Framework
- **Vue 3.5**: Progressive JavaScript Framework
- **Vite 5.4**: Next Generation Frontend Tooling

### Map Engine
- **CesiumJS 1.135**: 3D Globe and Map Engine
- **Vue-Cesium 3.2**: Vue 3 wrapper for CesiumJS
- **AMap (Gaode)**: Base map service (GCJ-02 coordinate system)

### Core Libraries
- **JSZip 3.10**: KMZ file compression/decompression
- **UUID**: Unique identifier generation (custom implementation)

## 📁 Project Structure

```
way_line/
├── src/
│   ├── components/
│   │   └── WaypointGenerator/
│   │       ├── index.vue              # Main Component
│   │       ├── MapViewer.vue          # Map View
│   │       ├── ControlPanel.vue       # Control Panel
│   │       ├── MissionConfig.vue      # Mission Config
│   │       └── WaypointList.vue       # Waypoint List
│   ├── utils/
│   │   ├── kmzGenerator.js            # KMZ Generator
│   │   ├── kmzParser.js               # KMZ Parser
│   │   ├── routePlanner.js            # Route Planning Algorithm
│   │   ├── coordTransform.js          # Coordinate Transform (GCJ-02 ↔ WGS84)
│   │   └── geoUtils.js                # Geographic Utils
│   ├── App.vue                        # App Root Component
│   └── main.js                        # App Entry
├── public/                            # Static Assets
├── package.json                       # Project Config
├── vite.config.js                     # Vite Config
└── README.md                          # Project Documentation
```

## 🔧 Core Algorithms

### Coordinate Transformation
The project implements mutual conversion between GCJ-02 (Mars Coordinate System) and WGS84 (GPS Coordinate System):

- **Storage**: Uses GCJ-02 coordinates (consistent with AMap)
- **Display**: Directly uses GCJ-02 coordinates (no offset)
- **Export**: Converts to WGS84 coordinates (DJI standard)

This ensures:
- ✅ Frontend click position and display position are completely consistent
- ✅ Imported into DJI, the position is accurate without offset

### S-shaped Scan Path Generation
Automatically generates S-shaped scanning paths based on polygon areas:

1. **Coordinate Projection**: Convert lat/lon to plane coordinates (meters)
2. **Polygon Shrink**: Shrink inward based on margin parameter
3. **Coordinate Rotation**: Rotate coordinate system based on direction angle
4. **Scan Line Generation**: Generate horizontal scan lines in the rotated coordinate system
5. **Intersection Calculation**: Calculate intersections between scan lines and polygon
6. **Path Optimization**: S-shaped connection, reducing turns
7. **Reverse Rotation**: Convert back to original coordinate system
8. **Coordinate Restoration**: Convert back to lat/lon

### Distance and Time Calculation
Uses **Haversine Formula** to calculate great-circle distance between waypoints:

```javascript
const R = 6371000; // Earth radius (meters)
const φ1 = lat1 * π / 180;
const φ2 = lat2 * π / 180;
const Δφ = (lat2 - lat1) * π / 180;
const Δλ = (lng2 - lng1) * π / 180;

const a = sin²(Δφ/2) + cos(φ1) · cos(φ2) · sin²(Δλ/2);
const c = 2 · atan2(√a, √(1−a));
const d = R · c;
```

## 📝 KMZ File Structure

The generated KMZ file complies with DJI WPML 1.0.6 standard:

```
mission.kmz
└── wpmz/
    ├── template.kml       # Template Definition (Area, Parameters)
    └── waylines.wpml      # Wayline Definition (Waypoints, Actions)
```

### template.kml
- Mission Config (Speed, Height Mode, Lost Control Action, etc.)
- Area Definition (Polygon Coordinates)
- AI Patrol Parameters (Direction, Margin, Overlap, Target Type)
- Gimbal and Camera Parameters

### waylines.wpml
- Waypoint List (Coordinates, Height, Speed)
- Waypoint Actions (Gimbal Pitch, Take Photo, Record Video)
- AI Target Detection Actions
- Route Statistics (Distance, Duration)

## ⚠️ Important Notes

### Coordinate System
- Frontend map uses **GCJ-02** (AMap)
- Exported KMZ uses **WGS84** (GPS Standard)
- System handles conversion automatically, no manual operation needed

### Height Settings
- **Absolute Height**: Need to know the actual altitude of the area
- **Relative to Takeoff**: Suitable for most scenarios
- **Relative to Ground**: Requires drone support for real-time ranging sensors

### AI Patrol
- Only supports **Matrice 4T** and above models
- Need to enable AI features in DJI FlightHub 2
- Recommended scan spacing 10-50m, adjust according to target size

### File Compatibility
- Generated KMZ files comply with **WPML 1.0.6** standard
- Compatible with DJI FlightHub 2 and Matrice series drones
- Recommended to backup original routes before importing

## 🐛 FAQ

### Q: Position offset after importing to DJI?
A: Solved by coordinate conversion. If offset persists, please check:
- Is the base map AMap?
- Is it within China (Coordinate conversion is only valid in China)?

### Q: AI patrol route shows as dashed line?
A: Dashed line indicates a template, solid line indicates a determined route. Added `distance` and `duration` parameters, should display as solid line.

### Q: Scan path direction is wrong?
A: Adjust **Route Direction Angle**:
- 0° = North-South (Vertical)
- 90° = East-West (Horizontal)

### Q: Too many waypoints generated?
A: Decreasing scan spacing or increasing overlap will increase waypoints. Recommended:
- Scan Spacing: 20-50m
- Overlap: Keep default 80%/70%

## 📄 License

This project is licensed under the **GPL-3.0 License** (GNU General Public License v3.0).

### Key Permissions

- ✅ **Commercial Use**: Commercial use is allowed
- ✅ **Modification**: Modification of source code is allowed
- ✅ **Distribution**: Distribution of original or modified versions is allowed
- ✅ **Patent Grant**: Provides explicit patent grant
- ✅ **Private Use**: Private use and modification is allowed

### Conditions

- ⚠️ **Same License**: Derivative works must use the same GPL-3.0 license
- ⚠️ **Open Source Requirement**: Must provide complete source code when distributing
- ⚠️ **Copyright Notice**: Must retain original author's copyright notice and license information
- ⚠️ **State Changes**: Must document modifications when files are changed

### Why GPL-3.0?

1. **Protect Open Source Ecosystem**: Ensures derivative works remain open source, preventing closed-source commercial use
2. **Patent Protection**: GPL-3.0 provides explicit patent grants, protecting users from patent litigation
3. **Promote Sharing**: Encourages developers to share improvements and advance the project together
4. **DRM Restriction**: Prohibits using DRM (Digital Rights Management) to restrict user rights

For full license text, please see the [LICENSE](./LICENSE) file.

## 🤝 Contribution

Issues and Pull Requests are welcome!

## 📧 Contact

- **WeChat**: `hecongyuan2025`
- **Email**: `h285121973@gmail.com`
- **Feedback**: Submit via GitHub Issues

<img src="doc/images/wechat_qr.jpg" width="200" alt="WeChat QR Code">

## 👥 Community Group

Welcome to join the DJI Waypoint Generator community group! Connect with other developers and users, share route planning tips, exchange experiences, and stay updated with the latest features!

<img src="doc/images/IMG_5215.JPG" width="300" alt="Community Group QR Code">
