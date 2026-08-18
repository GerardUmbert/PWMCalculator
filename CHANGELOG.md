# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Unreleased]

### Fixed
- Page was locked to a fixed-height, no-scroll layout on small screens, making content below the fold unreachable on mobile. Scroll locking now only applies on desktop-sized viewports.

### Changed
- Renamed the "New PRO Fan" profile to "New Fan".
- Consolidated the tool into a single `index.html` (removed the duplicate `pwm-fan-curve.html`).

### Added
- Initial public release of the PWM Fan Curve Comparator.
- README with usage documentation.
- GitHub Pages deployment workflow.
