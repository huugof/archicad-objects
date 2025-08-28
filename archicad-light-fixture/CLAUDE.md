# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a complete Archicad object library for a parametric square recessed light fixture. The project uses Archicad's GDL (Geometric Description Language) to create a fully customizable 3D light fixture with comprehensive 2D representation and user interface.

## Architecture

The light fixture object follows Archicad's standard GDL object structure with separate script files:

- `master.gdl` - Main object definition with parameter processing, coordinate system setup, and common variables
- `parameter.gdl` - Parameter validation, constraints, minimum/maximum limits, and UI behavior logic
- `interface.gdl` - Complete 3-column user interface layout with grouped controls for 3D options, dimensions, and 2D display
- `2d.gdl` - 2D symbol with square outline, multiple symbol styles, movable labels with rotation compensation, and opaque mask options
- `3d.gdl` - Full 3D geometry generation including tapered recess walls, exterior walls, top cap, optional flange ring, and lens
- `paramaters.csv` - Parameter definitions with types, names, and default values

## Key Features

### Parametric Geometry
- **Base/Top dimensions**: Independent control of bottom (`bX`, `bY`) and top (`tX`, `tY`) openings for tapered recesses
- **Square constraint**: `isSquare` parameter locks width/length ratios
- **Tapered walls**: `isTapered` parameter controls whether recess tapers from base to top
- **Wall thickness**: `wallThk` parameter with automatic constraint validation
- **Depth control**: `hDepth` parameter for recess depth

### Optional Components
- **Flange ring**: `hasFlange` toggle with thickness (`flThk`) and overhang (`flLap`) controls
- **Lens/glass**: `lensToggle` with setback distance control
- **Cap thickness**: `capThk` for solid top surface

### 2D Representation
- **Symbol styles**: 4 options (plain square, X pattern, crosshair, down arrow)
- **Smart labels**: Toggle between object ID and custom text with full rotation compensation
- **Opaque mask**: Optional filled background for better visibility
- **Movable hotspots**: Interactive label positioning

### Materials System
- **Fixture surface**: `matRecess` for main recess walls and cap
- **Flange surface**: `matFlange` for optional flange ring  
- **Lens material**: `matLens` for optional glass/lens component

## Development Notes

### Coordinate System
- Uses imperial units (inches)
- Z=0 is ceiling plane, recess extends upward (+Z direction)
- `originToggle` parameter can shift entire object down by depth amount
- Geometry is centered on origin in X/Y plane

### Parameter Validation
- Comprehensive minimum/maximum limits in `parameter.gdl`
- Wall thickness automatically constrained to fit within openings
- UI elements locked/unlocked based on feature toggles (square mode, flange, lens, etc.)
- Label size validation with reasonable defaults

### GDL Implementation Patterns
- Uses `RULED` surfaces for tapered wall geometry
- `PRISM_` for extruded components (cap, flange)
- Material assignments before geometry creation
- Proper coordinate transformations with `ADD2`, `ROT2`, `DEL` stack management
- Hotspot-based interactive editing in 2D view

### No External Build System
- Files are used directly in Archicad
- No compilation or build process required
- Parameter changes trigger automatic geometry regeneration