# Initializing a Project

If you have forked Mint to use as the toolchain for your own extension, `npm run init` helps you replace the template placeholder values with your own details in one shot.

## What it does

The `init` script walks you through a short interactive prompt, then makes the following changes:

- Updates `package.json` with your package name, description, author, and version.
- Removes every file from `src/` except `src/01-core.js` (including any subdirectories).
- Writes a fresh `src/manifest.json` with your extension's metadata.
- Prepends an initialization comment header to `src/01-core.js`.

## Running it

```bash
npm run init
```

You will be prompted for:

| Prompt                 | Example value                              | Notes                                         |
| ---------------------- | ------------------------------------------ | --------------------------------------------- |
| npm package name       | `my-cool-extension`                        | Kebab-case, valid npm name                    |
| Extension display name | `My Cool Extension`                        | Shown in Scratch's extension picker           |
| Description            | `Does cool things`                         | Short description                             |
| Author                 | `Jane Doe`                                 | Used in the manifest and build header         |
| Initial version        | `0.1.0`                                    | Must be a valid semver string                 |
| License                | `MIT`                                      | SPDX identifier                               |
| URL                    | `https://github.com/you/my-cool-extension` | Repository or homepage                        |
| Extension id           | `myCoolExtension`                          | camelCase, auto-derived from the display name |

Each prompt shows a default value in parentheses. Press Enter to accept the default.

After you confirm, the script prints a summary of the changes it will make and asks you to type `yes` before proceeding. Anything other than `yes` or `y` aborts without making any changes.

## After initialization

Once `init` finishes:

1. Review `src/manifest.json` and make sure all fields are correct.
2. Open `src/01-core.js` and update the extension `id` in `getInfo()` to match the id you chose.
3. Run `npm run build` to confirm everything builds cleanly.
4. Start adding your own blocks.

> [!NOTE]
>
> `init` only runs once cleanly — it will not overwrite the header in `src/01-core.js` if you run it a second time. If you want to re-initialize, delete the `// Initialized by npm run init` comment from `01-core.js` first.

## Input validation

The script validates your inputs before making any changes:

- The package name must be a valid npm package name (lowercase, kebab-case, optionally scoped).
- The version must be a valid semver string.
- The extension id must start with a letter and contain only letters and digits (no hyphens, underscores, or spaces).

If any input fails validation the script exits with an error and no files are modified.
