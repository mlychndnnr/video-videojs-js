# [4.3.0](https://github.com/mlychndnnr/video-videojs-js/compare/v4.2.8...v4.3.0) (2026-06-28)


### Features

* redention name depricated ([#21](https://github.com/mlychndnnr/video-videojs-js/issues/21)) ([4afbb2f](https://github.com/mlychndnnr/video-videojs-js/commit/4afbb2fa66ff629e5355bfd6ccf321fcb08896a0))

## [4.2.8](https://github.com/mlychndnnr/video-videojs-js/compare/v4.2.7...v4.2.8) (2026-06-28)


### Bug Fixes

* removed e2e file ([#18](https://github.com/mlychndnnr/video-videojs-js/issues/18)) ([7d17038](https://github.com/mlychndnnr/video-videojs-js/commit/7d17038799a079e6fb08c718e285f7e716453eec))

## [4.2.7](https://github.com/mlychndnnr/video-videojs-js/compare/v4.2.6...v4.2.7) (2026-06-24)


### Bug Fixes

* dispatch use-shared-publish.yml instead of calling it as a reusable job ([#15](https://github.com/mlychndnnr/video-videojs-js/issues/15)) ([6caf0e2](https://github.com/mlychndnnr/video-videojs-js/commit/6caf0e2420992461196edfc337d7c9e3a81baad1))

## [4.2.6](https://github.com/mlychndnnr/video-videojs-js/compare/v4.2.5...v4.2.6) (2026-06-24)


### Bug Fixes

* improve check-release logging to show version comparison detail ([56bbc0e](https://github.com/mlychndnnr/video-videojs-js/commit/56bbc0e25a2f6c28b7d51401ea953eb5063e59e9))

## [4.2.5](https://github.com/mlychndnnr/video-videojs-js/compare/v4.2.4...v4.2.5) (2026-06-24)


### Bug Fixes

* use always() to force publish job evaluation past conditional dependency ([fd80a34](https://github.com/mlychndnnr/video-videojs-js/commit/fd80a34fffc0123c604d1d0a651a88d6ae4c2e18))

## [4.2.4](https://github.com/mlychndnnr/video-videojs-js/compare/v4.2.3...v4.2.4) (2026-06-24)


### Bug Fixes

* remove check-release from publish job needs to prevent silent skip ([76f5e81](https://github.com/mlychndnnr/video-videojs-js/commit/76f5e817953471119a7192ccdda57fae2550c362))

## [4.2.3](https://github.com/mlychndnnr/video-videojs-js/compare/v4.2.2...v4.2.3) (2026-06-24)


### Bug Fixes

* restore .releaserc.json and prevent it from being committed in release PRs ([ed8b48e](https://github.com/mlychndnnr/video-videojs-js/commit/ed8b48ea091fd691ded2e3d5a9f85a457fca9765))

## [4.2.2](https://github.com/mlychndnnr/video-videojs-js/compare/v4.2.1...v4.2.2) (2026-06-24)


### Bug Fixes

* fix two bugs preventing Stage 1 from detecting version changes ([fb9c34a](https://github.com/mlychndnnr/video-videojs-js/commit/fb9c34a32a1c488303125288a76b155f3c1e5136))
* remove redundant if condition from publish reusable workflow job ([62b3848](https://github.com/mlychndnnr/video-videojs-js/commit/62b3848f37f0ef2035ec455b63ebc3a5832946c5))

## [4.2.1](https://github.com/newrelic/video-videojs-js/compare/v4.2.0...v4.2.1) (2026-06-18)

### Features

- **Quality/Rendition Change Tracking:** Added optional support for automatic rendition change detection and reporting
  - Integrated optional `videojs-contrib-quality-levels` plugin for quality level monitoring
  - Implemented automatic rendition change event tracking with bitrate information
  - Added lazy initialization of quality levels plugin support
  - Tracks old and new bitrate during quality transitions
  - Graceful fallback when quality levels plugin is not loaded

### Documentation

- **Quality/Rendition Tracking Guide:** Comprehensive documentation for enabling optional quality tracking
  - Installation instructions for `videojs-contrib-quality-levels` plugin
  - Detailed explanation of how the feature works
  - Console debugging information for troubleshooting
  - NRQL query examples for analyzing quality changes
  - Updated README with Quality/Rendition Tracking section
  - Feature Highlights section now includes rendition change tracking

## [4.2.0](https://github.com/newrelic/video-videojs-js/compare/v4.1.2...v4.2.0) (2026-06-10)

### Features

- **MediaTailor Custom CDN Support:** Replaced URL-based auto-detection with explicit opt-in
  - Customers now pass `mediatailor: true` (or `mediatailor: { trackingUrl, adSegmentPrefix }`) to enable the tracker — supports both default AWS hostnames and custom CDN domains
  - Added `MT_DEFAULT_AD_SEGMENT_PATH` (`/tm/`) constant for AWS-recommended CDN ad-segment path; ad segments rewritten to a custom CDN domain under `/tm/` are detected automatically
  - `isMediaTailorSegment()` now checks the default AWS segments hostname, the `/tm/` path, and an optional customer-supplied `adSegmentPrefix`
  - Threaded `adSegmentPrefix` through HLS (VHS) and DASH manifest parsing
  - Added explicit session initialisation via `mediatailor: { trackingUrl }` for POST `/v1/session/` flows

- **Ad Tracking Configuration:** Introduced `config.ad.type` to control ad tracker selection
  - Exposed `AD_TRACKING` constant with CSAI (flat value covering IMA / Brightcove IMA / Freewheel / generic) and SSAI sub-types (`DAI`, `MT`)
  - SSAI requires an explicit sub-type — each platform needs its own SDK and cannot be auto-detected
  - `SSAI.MT` implies `mediatailor: true`
  - When `config.ad.type` is unset, falls back to CSAI auto-detection with a warning (backward compatible for v4.1.2 users)
  - Co-located `segmentPrefix` and `trackingUrl` under `config.ad`
  - Added `DaiAdsTracker` to static exports

- **Logging Improvements:**
  - Exposed `VideojsTracker.Log` as a static so UMD callers can set log level
  - Logs active ad segment detection mode at tracker startup
  - Logs the matched ad segment detection path on first ad break (once per session)
  - Logs which CSAI framework was auto-detected (BrightcoveIma / IMA / Freewheel / generic)
  - Replaced `console.log/warn/error` with `nrvideo.Log` across MediaTailor files

### Bug Fixes

- **Buffer End:** Fixed buffer end handling in tracker
- **Plugin Registration:** Fixed `register-plugin.js` silently dropping the options object and not forwarding it to the `TrackerJS` constructor

### Documentation

- **README & SSAI Docs:** Updated for custom CDN support, clarified when `trackingUrl` and `adSegmentPrefix` overrides are needed, cleaned up `sessionId` references
- **SSAI Troubleshooting:** Corrected `adSegmentPrefix` references to `config.ad.segmentPrefix`

### Samples

- **MediaTailor Lab:** Rewrote sample app with a clean minimal UI — license key / app ID / playback URL / format toggle, smart Load button (handles both session init and direct playback URLs), NR log level toggle, debug log showing detected mode, credentials persisted in localStorage

## [4.1.2](https://github.com/newrelic/video-videojs-js/compare/v4.1.1...v4.1.2) (2026-05-11)

### Features

- **AWS MediaTailor Support:** Added comprehensive support for AWS MediaTailor SSAI with DASH
  - Implemented MediaTailor tracker with manifest polling and ad tracking
  - Added MediaTailor lab sample for testing and demonstration
  - Enhanced DASH support for MediaTailor integration
  - Added unit test cases for MediaTailor functionality
  - Improved MediaTailor tracker reliability and event handling

### Bug Fixes

- **Bitrate Data Types:** Updated bitrate data types for improved accuracy and consistency
- **Manifest Fetch Error Handling:** Added proper error handling for manifest fetch failures
- **MediaTailor Configuration:** Moved MediaTailor config variables to global scope for better accessibility

### Documentation

- **SSAI Documentation:** Updated SSAI documentation to include MediaTailor integration details
- **MediaTailor Naming:** Clarified MediaTailor helper and state naming conventions

### Build & Infrastructure

- **Release Workflow:** Standardized release workflow with smart detection
- **Dependencies:** Updated semantic-release dependencies and package-lock.json
- **Cleanup:** Removed unrelated test infrastructure files, scripts, and dependencies

## [4.1.1](https://github.com/newrelic/video-videojs-js/compare/v4.1.0...v4.1.1) (2026-04-17)

### Documentation

- **README.md:** Added Best Practices section (contentTitle, userId, custom attributes, gradual rollout with feature flags)
- **README.md:** Promoted Bitrate Metrics to top-level section with detailed table format and NRQL query examples
- **README.md:** Updated Data Model event descriptions to include heartbeats and media errors
- **README.md:** Fixed DATAMODEL.md link casing
- **README.md:** Updated Table of Contents with new sections (Prerequisites, Best Practices, Bitrate Metrics)
- **README.md:** Renamed Contributing to Contribute for consistency across trackers

## [4.1.0](https://github.com/newrelic/video-videojs-js/compare/v4.0.3...v4.1.0) (2026-04-08)

### Breaking Changes

- **Method Renames:** Bitrate methods renamed for clarity
  - `getMeasuredBitrate()` → `getSegmentDownloadBitrate()` - ABR bandwidth estimate from player stats
  - `getDownloadBitrate()` → `getNetworkDownloadBitrate()` - Instantaneous network throughput
  - **Note:** Most users won't be affected as these methods are primarily used internally by the tracker

### Deprecated

- **Removed `getRenditionBitrate()` method** - No longer needed with improved bitrate tracking system

### Enhancements

- **Bitrate Metrics Refactoring:**
  - Implemented consistent fallback pattern across all bitrate methods (VHS direct access → tech wrapper fallback)
  - Simplified network download bitrate to use direct throughput access
  - Enhanced bitrate tracking with four distinct metrics for comprehensive quality analysis
  - Updated all tech wrappers (VHS, hls.js, Shaka) with consistent implementations

- **Comprehensive Documentation Rewrite:**
  - **README.md:** Complete rewrite with professional structure, badges, features section, table of contents, two installation options, expanded API reference, and clear New Relic support channels
  - **datamodel.md:** Complete rewrite with comprehensive event reference, all four bitrate metrics definitions, QoE attributes, complete attribute tables for all event types, and SSAI/DAI support documentation
  - **DEVELOPING.md:** Complete development guide with setup, build instructions, project structure, testing guidelines, and release process
  - **REVIEW.md:** NEW FILE - Code review guidelines and standards for contributors

### Documentation

- Added clear instructions to obtain configuration from [one.newrelic.com](https://one.newrelic.com)
- Updated all bitrate metric definitions with accurate sources and use cases
- Added comprehensive API reference with method signatures and examples
- Enhanced support section with multiple New Relic support channels
- Added third-party library license disclosure

## [4.0.3](https://github.com/newrelic/video-videojs-js/compare/v4.0.2...v4.0.3) (2025-11-21)

### Bug Fixes

- removed github token ([f5f9ade](https://github.com/newrelic/video-videojs-js/commit/f5f9ade01c9af411d72ec74874f8d0750c5f0f66))

# CHANGELOG

## [4.0.2] - 2025-10-21

### Bug Fixes

- **Content Bitrate Detection:** Enhanced `getBitrate()` method with comprehensive Video.js tech support
  - Added VHS (Video HTTP Streaming) API support for HLS/DASH content
  - Implemented audio + video bitrate combination for total bandwidth calculation
  - Added fallback support for Shaka Player, HLS.js, and DASH.js
  - Improved bitrate detection reliability across different streaming technologies
  - Fixed issue where bitrate remained constant throughout video playback

## [4.0.1] - 2025-09-11

### Add

- Added methods for `Ad Bitrate` and `Ad Rendition Bitrate` in ima.js and dai.js

## [4.0.0] - 2025-08-26

### Major Updates:

- Upgraded `@newrelic/video-core` dependency to version `4.0.0`.
- Introduced support for SSAI (Server-Side Ad Insertion) Google DAI.
- Minor fixes to webpack configuration

## [3.1.0] - 2025-05-27

### Enhancements

- **Publishing to npm:** The package can now be published to npm, making it easily accessible.

### Build

- **Distribution Formats:** Added `cjs`, `esm`, and `umd` builds to the `dist` folder, ensuring compatibility with CommonJS, ES Modules, and UMD module formats.

## [3.0.1] - 2025-04-24

### Bug Fixes

- Resolved an issue where custom attribute definitions were not accepting options as arguments.
- **Update:** The `errorName` attribute has been deprecated and `errorMessage` is introduced as its replacement.

## [3.0.0] - 2025/02/20

### New Event Type Introduced [VideoAction, VideoErrorAction, VideoAdAction, VideoCustomAction]

- PageAction Deprecated.
- New Attributes Added,

## [0.7.1] - 2024/11/13

### Bug fix

- Added Null Handler in the `Tracker`.

## [0.7.0] - 2024/09/18

### Add

- Language attribute.

### Update

- Samples.

## [0.6.0] - 2024/05/17

### Update

- Update configuration stuff.

## [0.5.0] - 2020/05/04

### Fix

- Update dependencies to fix multiple vulnerabilities.

## [0.4.0] - 2020/04/16

### Add

- OS stuff.

### Update

- Video Core library.

## [0.3.1] - 2018/01/11

### Remove

- Remove old reference to `sendPlayerInit`.

## [0.3.0] - 2017/11/03

### Add

- Add support for `creativeId`, `adId` and `adPartner`.

## [0.2.0] - 2017/11/03

### Add

- Add support for `FreeWheel` ads.

## [0.1.2] - 2017/11/02

### Lib

- Update project to support core `0.5+`.

## [0.1.1] - 2017/10/23

### Fix

- Add aditional checks to `ima` tracker.

## [0.1.0]

- First Version
