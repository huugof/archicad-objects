# Ceiling Light Square - Development Notes

## Object Overview
Parametric square recessed light fixture with optional tapering and modular components.

## Key Parameters
- `bX/bY, tX/tY`: Bottom/top dimensions for tapered recess
- `isSquare`: Locks aspect ratio for perfect squares
- `isTapered`: Controls wall geometry (straight vs tapered)
- `hasFlange/lensToggle`: Optional components

## Known Issues
- None currently reported

## Recent Refinements
- Fixed parameter file spelling (paramaters.csv → parameters.csv)
- Reorganized build output to build/ directory

## Development Notes
- Square constraint system via isSquare parameter
- Independent X/Y sizing when square mode disabled
- Same material system as round variant
- 2D symbol includes multiple style options

## Testing Checklist
- [ ] Square constraint locks/unlocks properly
- [ ] Tapered vs straight wall geometry
- [ ] Parameter validation for wall thickness
- [ ] 2D symbol style variations
- [ ] Export consistency with round variant