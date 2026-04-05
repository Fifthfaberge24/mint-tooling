# Assets

Mint can embed images, sounds, and other binary files directly into your extension bundle as base64 data URIs. This means your extension is still a single self-contained `.js` file even when it uses icons or other media.

## Adding an asset

The easiest way is to use the asset manager:

```bash
npm run asset:add -- path/to/image.png
```

This copies the file into `src/assets/` and prints the usage snippet you need:

```
✓ Added src/assets/image.png  (image/png, 4.23 KB)

Usage snippet:
  __ASSET__('image.png')
```

You can also copy files into `src/assets/` manually. Subdirectories are fine:

```
src/assets/
  icons/
    menu.png
    block.png
  sounds/
    pop.wav
```

## Using an asset in your code

Reference an asset by its path relative to `src/assets/` using the `__ASSET__()` macro:

```js
menuIconURI: __ASSET__('icons/menu.png'),
blockIconURI: __ASSET__('icons/block.png'),
```

At build time, Mint replaces each `__ASSET__('...')` call with the corresponding base64 data URI string.

You can also use the runtime helper `__mint_getAsset` for cases where you need to check whether an asset exists before using it:

```js
menuIconURI:
  (typeof __mint_getAsset === 'function' && __mint_getAsset('icons/menu.png')) || '',
```

This pattern is what the template's `01-core.js` uses. It falls back to an empty string gracefully if the asset is not present.

> [!NOTE]
>
> `__ASSET__()` is a build-time macro — it is replaced by a string literal during bundling. `__mint_getAsset()` is a runtime function that is generated and injected by the bundler when assets are present. Both refer to the same data; the difference is when the lookup happens.

## Listing assets

```bash
npm run asset:list
```

Prints a table of every file in `src/assets/` with its MIME type and size:

```
+--------------+------------+----------+
| Name         | Type       | Size     |
+--------------+------------+----------+
| icons/block.png | image/png | 1.23 KB |
| icons/menu.png  | image/png | 0.98 KB |
+--------------+------------+----------+
2 asset(s) total.
```

## Removing an asset

```bash
npm run asset:remove -- icons/menu.png
```

Before deleting the file, the command scans top-level `.js` files directly under `src/` (it does not recurse into subdirectories) for `__ASSET__('icons/menu.png')` references. If it finds any, it aborts:

```
✗ Cannot remove 'icons/menu.png' — it is still referenced in:
  src/01-core.js
Remove or update those references first, then run this command again.
```

This prevents you from producing a build that references a missing asset.

## Supported file types

The bundler detects the MIME type from the file extension. Common types that are supported out of the box include:

| Extension       | MIME type       |
| --------------- | --------------- |
| `.png`          | `image/png`     |
| `.jpg`, `.jpeg` | `image/jpeg`    |
| `.gif`          | `image/gif`     |
| `.webp`         | `image/webp`    |
| `.svg`          | `image/svg+xml` |
| `.mp3`          | `audio/mpeg`    |
| `.wav`          | `audio/wav`     |
| `.ogg`          | `audio/ogg`     |

Files with an unrecognised extension are embedded as `application/octet-stream`.

## Build-time validation

Before bundling, the build script checks that every `__ASSET__('path')` reference in top-level `.js` files directly under `src/` resolves to an actual file in `src/assets/`. If a reference is broken, the build fails and lists the problematic references. Assets that exist in `src/assets/` but are not referenced anywhere produce a warning but do not stop the build.

You can run this check on its own without building:

```bash
npm run validate:assets
```
