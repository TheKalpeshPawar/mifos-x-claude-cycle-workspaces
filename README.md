# Mifos X Claude Cycle Workspaces

Project workspaces for Mifos X ecosystem projects using [claude-product-cycle](https://github.com/mobilebytesensei/claude-product-cycle) framework.

## Projects

| Project | Description | Source | Status |
|---------|-------------|--------|:------:|
| `mifos-mobile/` | KMP Self-Service Mobile Banking App | [openMF/mifos-mobile](https://github.com/openMF/mifos-mobile) | Active |

## Quick Start

### Option 1: Via Framework (Recommended)

```bash
# Clone framework with all workspaces
git clone --recursive git@github.com:mobilebytesensei/claude-product-cycle.git
cd claude-product-cycle

# Run setup script
./setup.sh
```

### Option 2: Clone This Workspace Directly

```bash
# Clone with submodules
git clone --recursive git@github.com:therajanmaurya/mifos-x-claude-cycle-workspaces.git

# Or clone and init submodules separately
git clone git@github.com:therajanmaurya/mifos-x-claude-cycle-workspaces.git
cd mifos-x-claude-cycle-workspaces
git submodule update --init --recursive
```

## Structure

```
mifos-x-claude-cycle-workspaces/
├── README.md
├── WORKSPACES_INDEX.md
└── mifos-mobile/
    ├── PROJECT.md                 # Project configuration
    ├── design-spec-layer/         # Feature specifications, mockups
    │   └── features/
    │       ├── auth/
    │       ├── home/
    │       └── ...
    ├── server-layer/              # API documentation (Fineract)
    ├── client-layer/              # Network/data layer tracking
    ├── feature-layer/             # UI layer tracking
    ├── platform-layer/            # Platform-specific tracking
    ├── testing-layer/             # Test tracking
    └── source/                    # ← Git submodule (openMF/mifos-mobile)
```

## Working with Submodules

### Update Source to Latest

```bash
cd mifos-mobile/source
git checkout development
git pull origin development
cd ../..
git add mifos-mobile/source
git commit -m "chore: update mifos-mobile source to latest"
```

### Switch Source Branch

```bash
cd mifos-mobile/source
git checkout feature/my-branch
```

### After Cloning (if submodules not initialized)

```bash
git submodule update --init --recursive
```

## Daily Workflow

```bash
# Start session
/session-start

# Check what needs work
/gap-analysis

# Work on features
/design auth
/implement auth

# End session
/session-end
```

## Related Projects

- [mifos-mobile](https://github.com/openMF/mifos-mobile) - Source code
- [Fineract](https://github.com/apache/fineract) - Backend API
- [claude-product-cycle](https://github.com/mobilebytesensei/claude-product-cycle) - Framework

## License

Apache 2.0 License (aligned with Mifos Initiative)
