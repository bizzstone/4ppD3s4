# Changelog


### Changed

- `AppCastItem` is now marked serializable
- If using `SecurityMode.Unsafe`, files are **always** redownloaded because the library has no good way of knowing whether or not the file that is on disk is the file that is actually on the server (@rolikoff)
- Fixed a bug where if you cancel the download process or if an error occurs during download, the update file stays in the same directory (@rolikoff)
- Fixed a bug where the `DownloadCanceled` event was fired twice (@rolikoff)

## [0.14.0] (Same as 0.14.0.1 because Deadpikle goofed)

### Added

- NetSparkle now supports the `sparkle:os` attribute (#17). If this is not present, an update is assumed to be a Windows update. Valid types for Windows are "win" or "windows". The operating system string check is a case-insensitive check.
    - Added `OperatingSystemString` (default "windows") and `bool IsWindowsUpdate` to `AppCastItem`
    - `AppCast.GetUpdates()` no longer returns non-Windows updates
- To increase compatibility with the main macOS Sparkle project, the `enclosure` tag can now be either `enclosure` or `sparkle:enclosure`
- Added `AppCastItem.MIMEType` to read the `<enclosure type="">` attribute if they want to (#15). Defaults to `application/octet-stream`.
- Added `UpdateDetectedEventArgs.AppCastItems` if you want to look at all available app cast items
- Added `DownloadPathForAppCastItem(AppCastItem item)` to easily grab the download path for a given downloadable appcast item
- Added `RunUpdate(AppCastItem item)` to allow you to run an update without waiting for the latest version to download. The DSA signature of the file is still checked!

### Changed

- `NetSparkle.UpdateSystemProfileInformation` is now private
- `AppCast` no longer takes a Sparkle object and instead takes only those parameters that it needs to operate
- `NextUpdateAction` is now in its own file in the `NetSparkle.Enums` namespace

### Removed

## [0.13.0] - 2017-12-06

### Added

- **BREAKING CHANGE** Added `HideRemindMeLaterButton()` to `IUpdateAvailable`
- **BREAKING CHANGE** Added `HideSkipButton()` to `IUpdateAvailable`
- Added `HideRemindMeLaterButton` to the `NetSparkle` class. Defaults to false. Set to true to make `NetSparkle` call `HideRemindMeLaterButton()` when showing the update window.
- Added `HideSkipButton` to the `NetSparkle` class. Defaults to false. Set to true to make `NetSparkle` call `HideSkipButton()` when showing the update window.
- Added `RemindMeLaterSelected` to the `NetSparkle` class. Defaults to null. Use this event to be notified when the user has clicked the `Remind Me Later` button in the update window. (@enscope)

### Changed

- Release notes are now downloaded asynchronously, which should speed up the time it takes to show the download window
- Release note date is now Date.ToString("D") instead of "dd MMM yyyy" so that release notes show localized date strings
- **POTENTIALLY BREAKING CHANGE** Fixed bug where `ValidationResult.Unchecked` was not returned properly from `OnDownloadFinished` if download file signature is null (@keithclanton)
- **BREAKING CHANGE** `IUpdateAvailable` now has a `Result` of type `UpdateAvailableResult` rather than `DialogResult` in order to remove a dependency on WinForms. Use `DefaultUIFactory.ConvertDialogResultToUpdateAvailableResult` to convert from `DialogResult` to `UpdateAvailableResult` if needed. (@enscope) 

### Removed

## [0.12.0] - 2017-08-02
### Added

- Added new `LogWriter` class for printing diagnostic messages to the console. You can now create your own child class that inherits from `LogWriter` to customize how information is logged to the console (or file, or wherever else you want diagnostic messages sent!)!
- Added .gitattributes file for line ending consistency for all developers (@stephenwade)