# Design Token Repository

This repository serves as the **source of truth** for design tokens exported from Figma.

## Purpose

This repository contains the raw design token exports from Figma. When tokens are updated in Figma and exported here, they trigger an automated build pipeline in the `design-token-lib` repository.

## File Structure

```
.
├── tokens-export.json    # Figma token export (DO NOT EDIT MANUALLY)
├── .github/
│   └── workflows/
│       └── validate.yml  # Validation workflow
└── README.md
```

## Workflow

1. **Export from Figma**: Designers export tokens from Figma as JSON
2. **Update this repo**: Replace `tokens-export.json` with the new export
3. **Automatic validation**: GitHub Actions validates the JSON syntax and structure
4. **Trigger build**: On successful validation, automatically triggers build in `design-token-lib`

## Token Structure

The `tokens-export.json` file must follow this structure:

```json
[
  {
    "theme-name": {
      "modes": {
        "light": {
          "token-name": {
            "$type": "color",
            "$value": "#ffffff",
            "$scopes": ["ALL_SCOPES"]
          }
        },
        "dark": {
          "token-name": {
            "$type": "color",
            "$value": "#000000",
            "$scopes": ["ALL_SCOPES"]
          }
        }
      }
    }
  }
]
```

## Validation Rules

The validation workflow checks:

- ✅ Valid JSON syntax
- ✅ File is an array
- ✅ At least one theme exists
- ✅ Each theme has a `modes` object
- ✅ Each theme has both `light` and `dark` modes
- ✅ Each token has `$type` and `$value` properties

## Updating Tokens

1. Export tokens from Figma
2. Replace `tokens-export.json` with the new export
3. Commit and push to the repository
4. The validation workflow will run automatically
5. If validation passes, the build pipeline in `design-token-lib` will be triggered

## Important Notes

- **DO NOT** manually edit `tokens-export.json` - always export from Figma
- **DO NOT** commit generated files or build artifacts
- This repository should only contain the source token file

## Related Repositories

- **design-token-lib**: Builds and publishes tokens as npm package
- **component-lib**: Consumes tokens and generates MUI themes

