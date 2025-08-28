# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an Archicad object development repository focused on parametric lighting fixtures. The project uses Archicad's GDL (Geometric Description Language) to create customizable 3D objects with comprehensive 2D representation and user interfaces. The primary workflow is developing new objects, refining existing ones, and maintaining a library of reusable patterns.

## Repository Structure

```
/objects/
├── CLAUDE.md                    # This development guide
├── _templates/                  # Starter templates for new objects
│   ├── basic-fixture/          # Simple fixture template
│   ├── parametric-template/    # Advanced parametric template  
│   └── README.md              # Template usage guide
├── ceiling-light-round/        # Circular recessed fixture
│   ├── parameters.csv         # Parameter definitions
│   ├── master.gdl            # Main object logic
│   ├── parameter.gdl         # Parameter validation
│   ├── interface.gdl         # User interface layout
│   ├── 2d.gdl                # 2D symbol generation
│   ├── 3d.gdl                # 3D geometry generation
│   ├── build/                # Compiled GSM output
│   └── NOTES.md              # Object-specific notes
└── ceiling-light-square/       # Square recessed fixture
    └── [same structure as round]
```

## GDL Object Architecture

Each Archicad object follows the standard GDL structure with separate script files:

- `master.gdl` - Main object definition with parameter processing, coordinate system setup, and common variables
- `parameter.gdl` - Parameter validation, constraints, minimum/maximum limits, and UI behavior logic
- `interface.gdl` - Complete user interface layout with grouped controls for 3D options, dimensions, and 2D display
- `2d.gdl` - 2D symbol generation with multiple styles, movable labels, rotation compensation, and opaque mask options
- `3d.gdl` - Full 3D geometry generation including walls, caps, optional components, and material assignments
- `parameters.csv` - Parameter definitions with types, names, and default values

## Current Objects

### ceiling-light-round/
Parametric circular recessed light fixture with:
- **Geometry**: Tapered circular recess with `bDia/tDia` (bottom/top diameter) control
- **Optional Components**: Flange ring, lens/glass with setback control
- **2D Symbol**: Circular outline with multiple label and style options
- **Materials**: Separate assignments for recess, flange, and lens surfaces

### ceiling-light-square/  
Parametric square recessed light fixture with:
- **Geometry**: Rectangular recess with `bX/bY, tX/tY` dimensions, optional `isSquare` constraint
- **Tapered Control**: `isTapered` parameter for straight vs tapered walls
- **Optional Components**: Same flange/lens system as round variant
- **2D Symbol**: Square outline with 4 symbol style variations

## Common Features Across Objects

### Parametric Geometry
- **Dimensional Control**: Independent base/top sizing for tapered recesses
- **Wall Systems**: Configurable thickness with automatic constraint validation
- **Depth Control**: `hDepth` parameter for recess depth from ceiling plane
- **Origin Control**: `originToggle` shifts entire object by depth amount

### Optional Components
- **Flange Ring**: `hasFlange` toggle with thickness (`flThk`) and overhang (`flLap`) controls
- **Lens/Glass**: `lensToggle` with setback distance control  
- **Cap System**: `capThk` for solid top surface thickness

### 2D Representation
- **Multiple Symbol Styles**: Various visual representations (plain, X pattern, crosshair, arrows)
- **Smart Labels**: Toggle between object ID and custom text with rotation compensation
- **Opaque Masking**: Optional filled background for visibility
- **Interactive Editing**: Hotspot-based label positioning

### Materials System
- **Surface Assignments**: `matRecess`, `matFlange`, `matLens` for different object zones
- **Consistent Numbering**: Material IDs maintained across object variants

## Development Workflow

### Creating New Objects
1. **Start from Template**: Copy `_templates/basic-fixture/` or `_templates/parametric-template/` to new directory
2. **Customize Parameters**: Edit `parameters.csv` with object-specific values and constraints
3. **Develop Geometry**: Modify `3d.gdl` for your specific geometry generation
4. **Design 2D Symbol**: Update `2d.gdl` for appropriate symbol representation
5. **Build UI**: Adjust `interface.gdl` for parameter grouping and layout
6. **Test & Refine**: Load in Archicad, test parameter ranges, export to GSM
7. **Document**: Update object's `NOTES.md` with key features and known issues

### Refining Existing Objects
1. **Check Issues**: Review `NOTES.md` for reported bugs or enhancement requests
2. **Edit Source**: Modify appropriate GDL script files for the change
3. **Test Changes**: Load in Archicad and verify parameter behavior
4. **Update Documentation**: Record refinements in object's `NOTES.md`
5. **Rebuild GSM**: Export updated object to `build/` directory

### Template Development
- Extract common patterns from successful objects into `_templates/`
- Update template documentation when useful patterns emerge
- Templates should represent best practices and proven approaches

## Technical Implementation

### Coordinate System Standards
- **Units**: Imperial (inches) throughout all objects
- **Origin**: Z=0 at ceiling plane, recess extends upward (+Z direction)
- **Centering**: Geometry centered on origin in X/Y plane
- **Origin Control**: `originToggle` parameter shifts entire object down by depth

### Parameter Validation Patterns
- Comprehensive min/max limits in `parameter.gdl`
- Wall thickness automatically constrained to fit within openings
- UI elements locked/unlocked based on feature toggles
- Label size validation with reasonable defaults
- Dependency chains (e.g., flange controls only active when `hasFlange` = true)

### GDL Implementation Best Practices
- **Tapered Geometry**: Use `RULED` surfaces for smooth tapered walls
- **Extruded Components**: Use `PRISM_` for caps, flanges, simple extrusions
- **Material Flow**: Assign materials before geometry creation
- **Transform Stack**: Proper `ADD2`, `ROT2`, `DEL` stack management
- **Interactive Elements**: Hotspot-based editing in 2D views
- **Performance**: Minimize complex calculations in tight loops

### Build and Deployment
- **No Build System**: GDL files used directly in Archicad
- **Live Development**: Parameter changes trigger automatic regeneration
- **GSM Export**: Manual export to `build/` directory for distribution
- **Version Control**: Track source GDL files, not compiled GSM files

## Debugging Common Issues

### Parameter Problems
- Check `parameter.gdl` for constraint conflicts
- Verify min/max ranges don't create impossible conditions
- Test extreme parameter values for geometry failures

### Geometry Issues
- Review coordinate transformations for proper stack management
- Check material assignments occur before geometry creation
- Verify RULED surfaces have proper point arrays

### UI Problems
- Ensure parameter names match between scripts
- Check conditional UI elements have proper dependencies
- Test UI behavior across different parameter combinations