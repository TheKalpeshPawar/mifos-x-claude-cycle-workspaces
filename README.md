# Claude Cycle Workspaces

Example project workspaces for [claude-product-cycle](https://github.com/mobilebytesensei/claude-product-cycle) framework.

## What's Included

| Project | Description | Status |
|---------|-------------|:------:|
| `mifos-mobile/` | KMP mobile banking app | Complete |

## Usage

### Option 1: Clone as your workspace

```bash
# In your claude-product-cycle directory
git clone git@github.com:mobilebytesensei/claude-cycle-workspaces.git workspaces
```

### Option 2: Use as reference

Browse the `mifos-mobile/` example to see how to structure your own projects.

## Structure

Each project follows the 5-layer lifecycle:

```
project-name/
├── PROJECT.md              # Project configuration
├── design-spec-layer/      # Feature specifications, mockups
├── server-layer/           # API documentation
├── client-layer/           # Network/data layer tracking
├── feature-layer/          # UI layer tracking
├── platform-layer/         # Platform-specific tracking
└── testing-layer/          # Test tracking
```

## Contributing

Want to add your public project as an example? Submit a PR!

## License

MIT License
