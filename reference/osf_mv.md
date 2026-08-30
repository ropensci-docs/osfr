# Move a file or directory

Use `osf_mv()` to move a file or directory to a new project, component,
or subdirectory.

## Usage

``` r
osf_mv(x, to, overwrite = FALSE, verbose = FALSE)
```

## Arguments

- x:

  An
  [`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
  containing a single file or directory.

- to:

  Destination where the file or directory will be moved. This can be one
  of the following:

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
[`osf_cp()`](https://docs.ropensci.org/osfr/reference/osf_cp.md),
[`osf_mkdir()`](https://docs.ropensci.org/osfr/reference/osf_mkdir.md),
[`osf_rm()`](https://docs.ropensci.org/osfr/reference/osf_rm.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# Create an example file to upload to our example project
project <- osf_create_project("Flower Data")

write.csv(iris, file = "iris.csv")
data_file <- osf_upload(project,"iris.csv")

# Create a new directory to move our file to
data_dir <- osf_mkdir(project, "data")

# Move the file to our data directory
data_file <- osf_mv(data_file, to = data_dir)

# Move our data directory to a new component
data_comp <- osf_create_component(project, title = "data", category = "data")
data_dir %>%
  osf_mv(to = data_comp) %>%
  osf_open()
} # }
```
