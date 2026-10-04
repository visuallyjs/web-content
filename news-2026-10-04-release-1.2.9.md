# Release 1.2.9

October 4, 2026 ·

<!-- -->

One min read

Release 1.2.9 is now available. In this release:

### General[​](#general "Direct link to General")

* Refactored bulk loader code to implement a 4x performance improvement
* Updated packages to remove the `publishConfig` section of the package.json. This improves the portability of the built artifacts, allowing them to be uploaded to private NPM repositories without retaining the reference to the VisuallyJs repository URL.
* Added support for `minZoom` and `maxZoom` options on overlays: overlays can now be hidden/shown based upon the zoom level of the UI.
