# Upload files to OSF

Upload local files to a project, component, or directory on OSF.

## Usage

``` r
osf_upload(
  x,
  path,
  recurse = FALSE,
  conflicts = "error",
  progress = FALSE,
  verbose = FALSE
)
```

## Arguments

- x:

  The upload destination on OSF. Can be one of the following:

  - An
    [`osf_tbl_node`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
    with a single project or component.

  - An
    [`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
    with a single directory.

- path:

  A character vector of paths pointing to existing local files
  and/directories.

- recurse:

  If `TRUE`, fully recurse directories included in `path`. You can also
  control the number of levels to recurse by specifying a positive
  number.

- conflicts:

  This determines what happens when a file with the same name exists at
  the specified destination. Can be one of the following:

  - `"error"` (the default): throw an error and abort the file transfer
    operation.

  - `"skip"`: skip the conflicting file(s) and continue transferring the
    remaining files.

  - `"overwrite"`: replace the existing file with the transferred copy.

- progress:

  Logical, if `TRUE` progress bars are displayed for each file transfer.
  Mainly useful for transferring large files. For tracking lots of small
  files, setting `verbose = TRUE` is more informative.

- verbose:

  Logical, indicating whether to print informative messages about
  interactions with the OSF API (default `FALSE`).

## Value

An [`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
containing the uploaded files and directories that were directly
specified in `path`.

## File and directory paths

The `x` argument indicates *where* on OSF the files will be uploaded
(*i.e.*, the destination). The `path` argument indicates *what* will be
uploaded, which can include a combination of files *and* directories.

When `path` points to a local file, the file is uploaded to the *root*
of the specified OSF destination, regardless of where it's on your local
machine (*i.e.*, the intermediate paths are not preserved). For example,
the following would would upload both `a.txt` and `b.txt` to the root of
`my_proj`:

    osf_upload(my_proj, c("a.txt", "subdir/b.txt"))`

When `path` points to a local directory, a corresponding directory will
be created at the root of the OSF destination, `x`, and any files within
the local directory are uploaded to the new OSF directory. Therefore, we
could maintain the directory structure in the above example by passing
`b.txt`'s parent directory to `path` instead of the file itself:

    osf_upload(my_proj, c("a.txt", "subdir2"))

Likewise, `osf_upload(my_proj, path = ".")` will upload your entire
current working directory to the specified OSF destination.

## Uploading to subdirectories

In order to upload directly to an existing OSF directory you would first
need to retrieve the directory as an
[`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md).
This can be accomplished by passing the directory's unique identifier to
[`osf_retrieve_file()`](https://docs.ropensci.org/osfr/reference/osf_retrieve.md),
or, if you don't have the ID handy, you can use
[`osf_ls_files()`](https://docs.ropensci.org/osfr/reference/osf_ls_files.md)
to retrieve the directory by name.

    # search for the 'rawdata' subdirectory within top-level 'data' directory
    target_dir <- osf_ls_files(my_proj, path = "data", pattern = "rawdata")
    # upload 'a.txt' to data/rawdata/ on OSF
    osf_upload(target_dir, path = "a.txt")

## A note about synchronization

While
[`osf_download()`](https://docs.ropensci.org/osfr/reference/osf_download.md)
and `osf_upload()` allow you to conveniently shuttle files back and
forth between OSF and your local machine, it's important to note that
**they are not file synchronization functions**. In contrast to
something like [`rsync`](https://rsync.samba.org),
[`osf_download()`](https://docs.ropensci.org/osfr/reference/osf_download.md)/`osf_upload()`
do not take into account a file's contents or modification time. Whether
you're uploading or downloading, if `conflicts = "overwrite"`, osfr will
overwrite the existing file regardless of whether it is the more recent
copy. You have been warned.

## See also

- [`osf_download()`](https://docs.ropensci.org/osfr/reference/osf_download.md)
  for downloading files and directories from OSF.

- [`osf_ls_files()`](https://docs.ropensci.org/osfr/reference/osf_ls_files.md)
  for listing files and directories on OSF.

## Examples

``` r
if (FALSE) { # \dontrun{
# Create an example file to upload to our example project
write.csv(iris, file = "iris.csv")
project <- osf_create_project("Flower Data")

# Upload the first version
osf_upload(project,"iris.csv")

# Modify the data file, upload version 2, and view it on OSF
write.csv(subset(iris, Species != "setosa"), file = "iris.csv")
project %>%
  osf_upload("iris.csv", conflicts = "overwrite") %>%
  osf_open()
} # }
```
