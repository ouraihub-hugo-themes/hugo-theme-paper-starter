# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased]

### Changed
- Updated theme to v0.5.0 with Hugo Modules best practices
- Removed temporary layout overrides (index.html, baseof.html)
- Theme now works correctly as Hugo Module without workarounds
- Removed _vendor from git tracking (users should run `hugo mod vendor` after cloning)
- Updated .gitignore to exclude _vendor directory
- go.mod and go.sum are now properly tracked

### Fixed
- HTML pages now generate properly when using theme as Hugo Module
- No more "Page Not Found" errors on homepage
- Fixed incorrect .gitignore that was excluding go.mod and go.sum

## [v0.5.0] - 2025-01-14

### Added
- Hugo Modules best practices implementation in theme
- Proper mounts configuration via module.toml
- Clean configuration files without project-specific settings

### Changed
- Theme configuration cleaned up (removed contentDir, baseURL, etc.)
- Languages configuration moved to exampleSite
- Theme now follows Hugo official recommendations

### Fixed
- Fixed issue where HTML files were not generated
- Fixed configuration conflicts between theme and user project
- Fixed multilingual configuration issues

## Previous Versions

See theme repository for earlier version history.
