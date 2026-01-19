# Install
- macOS/Linux:
  - `curl -fsSL https://raw.githubusercontent.com/american-sensing/kicad-component-importer/main/scripts/install.sh | sh`
- Windows (PowerShell):
  - `iwr -useb https://raw.githubusercontent.com/american-sensing/kicad-component-importer/main/scripts/install.ps1 | iex`

# Quick start
Run from your KiCad project directory (the folder containing `*.kicad_pro`):
```sh
kicad-component-importer import /path/to/vendor.zip
```

This will:
- Create `project_symbols.kicad_sym`, `project_footprints.pretty`, and `project_3d` if missing.
- Import symbols/footprints from the zip or folder.
- Set each symbol's `Footprint` property to point at the new footprint.
- Create/update `sym-lib-table` and `fp-lib-table` so KiCad sees the libraries.

If your project has `my_project.kicad_pro`, defaults become:
- `my_project_symbols.kicad_sym`
- `my_project_footprints.pretty`
- `my_project_step`

# Configuration
On first run, a `.kci_config` file is written in the project directory.
You can edit it or override values via flags.

Example `.kci_config`:
```toml
symbol_lib = "project_symbols.kicad_sym"
footprint_lib = "project_footprints.pretty"
step_dir = "project_3d"
```

# CLI reference
```sh
kicad-component-importer import <SOURCE> \
  [--symbol-lib <SYMBOL_LIB>] \
  [--footprint-lib <FOOTPRINT_LIB>] \
  [--step-dir <STEP_DIR>]
```

- `<SOURCE>` can be a zip file or a folder containing `.kicad_sym` and `.kicad_mod` files.
- `--symbol-lib` points to a `.kicad_sym` file.
- `--footprint-lib` points to a `.pretty` directory.
- `--step-dir` points to a directory for 3D files (copied, not yet associated).

# Examples
Import from a zip:
```sh
kicad-component-importer import ~/Downloads/ul_ATSAMD11C14A-SSNT.zip
```

Override defaults:
```sh
kicad-component-importer import ./vendor_parts \
  --symbol-lib ./libs/my_symbols.kicad_sym \
  --footprint-lib ./libs/my_footprints.pretty \
  --step-dir ./libs/3d
```
