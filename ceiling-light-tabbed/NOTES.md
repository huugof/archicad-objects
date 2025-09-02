# Square Recessed Light - Tabbed Interface Version

## Overview

This is a tabbed interface version of the square recessed light fixture, demonstrating how to implement multi-tab GDL interfaces similar to Archicad's standard UI patterns.

## Tabbed Interface Implementation

### Key Components

1. **Tab Control Parameter**: `gs_ui_current_page` (hidden integer parameter)
   - Required for GDL's hierarchical tab system
   - Default value: 1 (first tab)

2. **Tab ID Constants** (in master.gdl):
   - `TABID_ROOT = 1` - Root level
   - `TABID_VISUALIZATION = 2` - 3D options and materials
   - `TABID_CONNECTIONS = 3` - Dimensions and connections
   - `TABID_PLAN_SYMBOL = 4` - 2D symbol and labels

3. **Tab Structure** (in interface.gdl):
   - Uses `UI_PAGE` commands with hierarchical structure
   - Conditional content display based on `gs_ui_current_page`

### Tab Organization

#### Tab 1: Visualization
- **3D Options**: Surface/recessed toggle, square/rectangle mode, tapered sides, flange/lens toggles, wall mount
- **Materials**: Fixture, flange, and lens surface assignments

#### Tab 2: Connections  
- **Dimensions**: Bottom/top width/length, height control
- **Connection Details**: Wall thickness, flange thickness/overhang, lens setback

#### Tab 3: Plan Symbol
- **Label Settings**: ID/custom toggle, custom text, pen, font size
- **Symbol Settings**: Style, opaque toggle, fill type, fill pen

## Technical Details

### Implementation Method
- Uses GDL's recommended "Hierarchical Pages" approach
- Automatic tab navigation provided by Archicad
- Maintains 444x296 pixel constraint per tab
- Preserves all existing parameter functionality and conditional visibility

### Advantages Over Single-Page Interface
- **Better Organization**: Logical grouping of related controls
- **Cleaner Layout**: Less cluttered interface
- **Professional Appearance**: Matches Archicad's standard UI patterns
- **Scalability**: Easy to add new tabs for additional features
- **Better Use of Space**: Each tab can utilize full available area

## Usage Notes

- All existing parameters and functionality are preserved
- Parameter validation and dependencies work the same as original
- Compatible with existing 3D and 2D scripts without modification
- Can be loaded in Archicad and exported as GSM for distribution

## Future Enhancements

- Additional tabs can be easily added (e.g., "3D View" tab for display options)
- Tab icons can be added using 18x18 pixel PNG images
- Advanced features can be grouped into separate tabs without cluttering main interface

This implementation demonstrates best practices for creating professional, organized GDL interfaces that scale well with complex parametric objects.