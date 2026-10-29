# Copy a file or directory

Use `osf_cp()` to make a copy of a file or directory in a new location.

## Usage

``` r
osf_cp(x, to, overwrite = FALSE, verbose = FALSE)
```

## Arguments

- x:

  An
  [`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
  containing a single file or directory.

- to:

  Destination where the file or directory will be copied. This can be
  one of the following:

  - An
    [`osf_tbl_node`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
    with a single project or component.

  - An
    [`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
    with a single directory.

- overwrite:

  Logical, if a file or directory with the same name already exists at
  the destination should it be replaced with `x`?

- verbose:

  Logical, indicating whether to print informative messages about
  interactions with the OSF API (default `FALSE`).

## Value

An [`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
containing the updated OSF file.

## Details

Note that a file (or directory) cannot be moved or copied onto itself,
even if `overwrite = TRUE`.

## See also

Other OSF file operations:
[`osf_mkdir()`](https://docs.ropensci.org/osfr/reference/osf_mkdir.md),
[`osf_mv()`](https://docs.ropensci.org/osfr/reference/osf_mv.md),
[`osf_rm()`](https://docs.ropensci.org/osfr/reference/osf_rm.md)

## Examples

``` r
if (FALSE) { # \dontrun{
project <- osf_create_project("Flower Data")

write.csv(iris, file = "iris.csv")
data_file <- osf_upload(project,"iris.csv")

# Create a new directory to copy our file to
data_dir <- osf_mkdir(project, "data")

# Copy the file to our data directory
data_file <- osf_cp(data_file, to = data_dir)

# Copy directory to new component
data_comp <- osf_create_component(project, title = "data", category = "data")
data_dir %>%
  osf_cp(to = data_comp) %>%
  osf_open()
} # }
```
