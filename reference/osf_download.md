# Download files and directories from OSF

Files stored on OSF can be downloaded locally by passing an
[`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
that contains the files and folders of interest. Use `path` to specify
*where* the files should be downloaded, otherwise they are downloaded to
your working directory by default.

## Usage

``` r
osf_download(
  x,
  path = NULL,
  recurse = FALSE,
  conflicts = "error",
  verbose = FALSE,
  progress = FALSE
)
```

## Arguments

- x:

  An
  [`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
  containing a single file or directory.

- path:

  Path pointing to a local directory where the downloaded files will be
  saved. Default is to use the current working directory.

- recurse:

  Applies only to OSF directories. If `TRUE`, a directory is fully
  recursed and all nested files and subdirectories are downloaded.
  Alternatively, a positive number will determine the number of levels
  to recurse.

- conflicts:

  This determines what happens when a file with the same name exists at
  the specified destination. Can be one of the following:

  - `"error"` (the default): throw an error and abort the file transfer
    operation.

  - `"skip"`: skip the conflicting file(s) and continue transferring the
    remaining files.

  - `"overwrite"`: replace the existing file with the transferred copy.

- verbose:

  Logical, indicating whether to print informative messages about
  interactions with the OSF API (default `FALSE`).

- progress:

  Logical, if `TRUE` progress bars are displayed for each file transfer.
  Mainly useful for transferring large files. For tracking lots of small
  files, setting `verbose = TRUE` is more informative.

## Value

The same
[`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
passed to `x` with a new column, `"local_path"`, containing paths to the
local files.

## Implementation details

Directories are always downloaded from OSF as zip files that contain its
entire contents. The logic for handling conflicts and recursion is
implemented locally, acting on these files in a temporary location and
copying them to `path` as needed. This creates a *gotcha* if you're
downloading directories with large files and assuming that setting
`conflicts = "skip"` and/or limiting recursion will reduce the number of
files you're downloading. In such a case, a better strategy would be to
use
[`osf_ls_files()`](https://docs.ropensci.org/osfr/reference/osf_ls_files.md)
to list the contents of the directory and pass that output to
`osf_download()`.

## A note about synchronization

While `osf_download()` and
[`osf_upload()`](https://docs.ropensci.org/osfr/reference/osf_upload.md)
allow you to conveniently shuttle files back and forth between OSF and
your local machine, it's important to note that **they are not file
synchronization functions**. In contrast to something like
[`rsync`](https://rsync.samba.org),
`osf_download()`/[`osf_upload()`](https://docs.ropensci.org/osfr/reference/osf_upload.md)
do not take into account a file's contents or modification time. Whether
you're uploading or downloading, if `conflicts = "overwrite"`, osfr will
overwrite the existing file regardless of whether it is the more recent
copy. You have been warned.

## See also

- [`osf_upload()`](https://docs.ropensci.org/osfr/reference/osf_upload.md)
  for uploading files to OSF.

- [`osf_ls_files()`](https://docs.ropensci.org/osfr/reference/osf_ls_files.md)
  for listing files and directories on OSF.

## Examples

``` r
if (FALSE) { # \dontrun{
# download a single file
analysis_plan <- osf_retrieve_file("2ryha") %>%
  osf_download()

# verify the file was downloaded locally
file.exists(analysis_plan$local_path)
} # }
```
