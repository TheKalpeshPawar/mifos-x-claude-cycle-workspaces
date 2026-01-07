# Mifos X Claude Cycle Workspaces

Project workspaces for Mifos X ecosystem projects using [claude-product-cycle](https://github.com/mobilebytesensei/claude-product-cycle) framework.

## Projects

| Project | Description | Status |
|---------|-------------|:------:|
| `mifos-mobile/` | KMP Self-Service Mobile Banking App | Active |

## Usage

```bash
# In your claude-product-cycle directory
git clone git@github.com:therajanmaurya/mifos-x-claude-cycle-workspaces.git workspaces

# Set active project
echo "mifos-mobile" > ACTIVE_PROJECT

# Start working
/session-start
/gap-analysis
```

## Structure

Each project follows the 5-layer lifecycle:

```
project-name/
├── PROJECT.md              # Project configuration
├── design-spec-layer/      # Feature specifications, mockups
├── server-layer/           # API documentation (Fineract)
├── client-layer/           # Network/data layer tracking
├── feature-layer/          # UI layer tracking
├── platform-layer/         # Platform-specific (Android, iOS, Desktop, Web)
└── testing-layer/          # Test tracking
```

## Related Projects

- [mifos-mobile](https://github.com/openMF/mifos-mobile) - Source code
- [Fineract](https://github.com/apache/fineract) - Backend API
- [claude-product-cycle](https://github.com/mobilebytesensei/claude-product-cycle) - Framework

## License

Apache 2.0 License (aligned with Mifos Initiative)
