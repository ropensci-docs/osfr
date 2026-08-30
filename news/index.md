# Changelog

## osfr (development version)

### Improvements

- Authentication errors (401/403) now include troubleshooting hints.
- Non-auth API errors now include the detail message from the API
  response.
- [`osf_auth()`](https://docs.ropensci.org/osfr/reference/osf_auth.md)
  warns if the provided PAT has an unexpected length.

### Fixes

- Fixed the `Accept` header name in `.build_client()`. The header was
  incorrectly set as `Accept-Header`, which meant API version pinning
  never actually worked.
- Fixed [`osf_mv()`](https://docs.ropensci.org/osfr/reference/osf_mv.md)
  and [`osf_cp()`](https://docs.ropensci.org/osfr/reference/osf_cp.md)
  failing with an uninformative error when a conflict is encountered.
  Waterbutler dropped the `code` field from conflict (409) responses,
  which prevented the error message from being extracted and surfaced
  correctly.

### API compatibility

- API requests are now pinned to OSF API version 2.20.

### Build and test infrastructure

- Updated vcr dependency to 2.0 and leverage new helpers:
  [`vcr::vcr_test_path()`](https://docs.ropensci.org/vcr/reference/vcr_test_path.html)
  and
  [`vcr::vcr_configure_log()`](https://docs.ropensci.org/vcr/reference/vcr_configure_log.html).
- Removed `filter_sensitive_data` since vcr 2.x auto-strips
  `Authorization` headers from cassettes.

## osfr 0.2.9

CRAN release: 2022-09-25

### Minor changes

- tibble v3.0.0 is now the minimum required version

### Fixes

- Fixed bug preventing uploads directly to OSF directories that
  contained conflicting files
  ([\#121](https://github.com/ropensci/osfr/issues/121),
  [\#129](https://github.com/ropensci/osfr/issues/129))
- Fixed pkgdown site build
  ([\#147](https://github.com/ropensci/osfr/issues/147))
- Fixed downloading of files via GUIDs
  ([\#141](https://github.com/ropensci/osfr/issues/141), thanks
  [@psanker](https://github.com/psanker))

### Build and test infrastructure

- Unit tests for single file uploads, html encoding, and basic node
  mechanics are now mocked with `vcr`
  ([\#145](https://github.com/ropensci/osfr/issues/145))
- GitHub Actions is now used for continuous integration
  ([\#146](https://github.com/ropensci/osfr/issues/146))
- brio is now used in tests for writing text to files so `\n` is used
  for line endings on Windows. This produces files with identical sizes
  on all platforms allowing vcr to match requests that include file
  sizes in the body
  ([\#146](https://github.com/ropensci/osfr/issues/146)).

## osfr 0.2.8

CRAN release: 2020-02-17

- Initial CRAN release
- Publication of accompanying paper in the [Journal of Open Source
  Software](https://joss.theoj.org/) that can be cited in papers using
  osfr, see `citation("osfr")` for details

### Minor changes

- Add rOpenSci reviewers to DESCRIPTION
- Remove deleted URLs from vignette
- Add badges for zenodo and JOSS
- Add `Makefile` for common developer tasks

## osfr 0.2.7

### Important changes

osfr is now part of rOpenSci and the documentation website has moved to
a new URL: <https://docs.ropensci.org/osfr/>.

### New features

- New [`osf_cp()`](https://docs.ropensci.org/osfr/reference/osf_cp.md)
  function for copying files to new locations
  ([@tpyork](https://github.com/tpyork),
  [\#114](https://github.com/ropensci/osfr/issues/114))

### Other changes

- The *getting started* vignette was overhauled to better leverage
  multi-file transfers and is now precomputed
- Encoded HTML symbols in node titles are now handled properly
  ([\#117](https://github.com/ropensci/osfr/issues/117))
- [`osf_rm()`](https://docs.ropensci.org/osfr/reference/osf_rm.md)
  argument `recursive` been renamed to `recurse` in order to be
  consistent with other functions
- Internal links now point to the ropensci repository and new
  documentation URL

## osfr 0.2.6

### Improved uploading

- New approach uses a file manifest to compare local and remote files
- We now search for conflicting remote files within each directory
  queued for upload, this avoids the issue reported in
  ([\#108](https://github.com/ropensci/osfr/issues/108), thanks
  [@tpyork](https://github.com/tpyork))

### osfr 0.2.6.1

- Fix pkgdown deployment

### osfr 0.2.6.2

- Fix project creation on windows
  ([\#110](https://github.com/ropensci/osfr/issues/110))
- Fix tests when PAT is undefined

### osfr 0.2.6.3

- Add JOSS paper

## osfr 0.2.5

### Multi-file transfers!

[`osf_download()`](https://docs.ropensci.org/osfr/reference/osf_download.md)
and
[`osf_upload()`](https://docs.ropensci.org/osfr/reference/osf_upload.md)
are now vectorized, making the process of adding files to or retrieving
files from OSF much more convenient. This functionality required
significant refactoring and brings with it several notable breaking
changes (see below).

### Other new features

- [`osf_download()`](https://docs.ropensci.org/osfr/reference/osf_download.md)
  and
  [`osf_upload()`](https://docs.ropensci.org/osfr/reference/osf_upload.md)
  gain the option to display progress bars.
- New
  [`osf_refresh()`](https://docs.ropensci.org/osfr/reference/osf_refresh.md)
  to update an existing `osf_tbl`.
- Devs can now enable logging API requests and responses by
  defining`OSF_LOG` (see Contributing for more information).

### Breaking changes

- [`osf_download()`](https://docs.ropensci.org/osfr/reference/osf_download.md)
  and
  [`osf_upload()`](https://docs.ropensci.org/osfr/reference/osf_upload.md)’s
  `overwrite` argument has been replaced with `conflicts`, which can be
  set to `"error"` (the default), `"skip"`, or `"overwrite"`.
- [`osf_upload()`](https://docs.ropensci.org/osfr/reference/osf_upload.md)’s
  `name` argument has been removed, so it is no longer possible to
  upload a file *and* change it’s OSF name.
- [`osf_download()`](https://docs.ropensci.org/osfr/reference/osf_download.md)’s
  `path` argument must point to an existing directory where all
  downloaded files will be saved.
- [`osf_download()`](https://docs.ropensci.org/osfr/reference/osf_download.md)’s
  `decompress` argument has been removed. The zip file downloaded from
  OSF is always decompressed in a temp directory where the enclosed
  files are selectively copied to the specified `path`.

### Minor changes

- Better error message when user attempts to upload directly to a file
  ([\#102](https://github.com/ropensci/osfr/issues/102),
  [@tiernanmartin](https://github.com/tiernanmartin)).
- crul v0.7.4 is now the minimum required version.
- The waterbutler client will now re-attempt failed requests 3 times.
- Consolidated internal client constructors.
- Increased wait time on travis to avoid time outs during testing.

## osfr 0.2.4

### Minor fixes

- Listing files within a specified `path` would fail if sibling
  directories shared a common substring in their names
  ([\#95](https://github.com/ropensci/osfr/issues/95))
- Setting `verbose=TRUE` now works properly for
  [`osf_upload()`](https://docs.ropensci.org/osfr/reference/osf_upload.md)
- A startup message is printed when `OSF_SERVER` is defined
- Improved documentation for `n_max`, GUIDs and the mysterious `meta`
  column

## osfr 0.2.3

### New features

- Failed OSF API requests are now re-attempted 3 times (requires crul
  v0.7.0)

### Minor fixes

- Fix incorrect column name in empty `osf_tbl`s
  ([\#88](https://github.com/ropensci/osfr/issues/88),
  [@machow](https://github.com/machow))
- No longer importing `modify_at()`
- Add rOpenSci badge
  ([\#89](https://github.com/ropensci/osfr/issues/89),
  [@maelle](https://github.com/maelle))
- Don’t build vignettes on travis

## osfr 0.2.2

### New features

- Added [`osf_mv()`](https://docs.ropensci.org/osfr/reference/osf_mv.md)
  to move files and directories to a new project, component, or
  subdirectory
- [`osf_rm()`](https://docs.ropensci.org/osfr/reference/osf_rm.md) can
  now delete files and directories

### Minor improvements and fixes

- Restructured tests to better handle environments in which `OSF_PAT`
  and/or `OSF_SERVER` are not defined

## osfr 0.2.1

- Minor tweaks to the website
- [`osf_retrieve_file()`](https://docs.ropensci.org/osfr/reference/osf_retrieve.md)
  will no longer retrieve files on 3rd-party storage providers, since
  other osfr functions currently only support OSF storage

## osfr 0.2.0

**NOTE:** This version of osfr is a rewrite of the original codebase. It
is effectively an entirely different package and provides no backwards
compatibility with functions in versions \< 0.2.0. The last version of
the previous package can be installed with the *remotes* package:

``` r

remotes::install_github("ropensci/osfr@v0.1.1")
```

See <https://docs.ropensci.org/osfr/> for details about the new package.
