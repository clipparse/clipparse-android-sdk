# Changelog

All notable changes to the ClipParse Android SDK will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.2.0] - 2026-11-23

### Added

- `ClipParseClient.extract(url)`, which extracts a recipe from a post URL.

### Changed

- More reliable TikTok extraction.
- [DATA_SAFETY.md](DATA_SAFETY.md) now covers TikTok links.

### Deprecated

- `ClipParseClient.extract(url, caption)`. Its `caption` parameter has no effect: call `extract(url)` instead. The function will be removed in a future major version.

## [1.1.0] - 2026-11-13

### Added

- `Ingredient.quantityMin` and `Ingredient.quantityMax`, the two ends of an amount given as a range ("3-4 tbsp" is 3 and 4), in the ingredient's `unit`. Both are set for a range and both are `null` for a single amount. `Ingredient.quantity` is unchanged: for a range it is the midpoint (3.5).

## [1.0.0] - 2026-11-12

### Added

- Initial release of the ClipParse SDK for Android 6.0 (API level 23) and later, distributed as an Android library on Maven Central: `com.clipparse:clipparse-android-sdk`.
- `ClipParseClient` with the suspending `extract` function, for extracting structured recipes (ingredients, steps, servings, timings) from TikTok and Instagram video links.
- `ExtractionResult`, which tells a recipe (`Success`) apart from a post that contains none (`NoRecipe`).
- `ClipParseException`, thrown on failure, with a `code` to tell errors apart, an `isRetryable` flag for transient failures, and `retryAfter` for when to try again.
- [DATA_SAFETY.md](DATA_SAFETY.md), which lists what the SDK sends and to whom, to help fill in Google Play's Data safety form.

[1.2.0]: https://github.com/clipparse/clipparse-android-sdk/releases/tag/1.2.0
[1.1.0]: https://github.com/clipparse/clipparse-android-sdk/releases/tag/1.1.0
[1.0.0]: https://github.com/clipparse/clipparse-android-sdk/releases/tag/1.0.0
