# Create directories on OSF

Use `osf_mkdir()` to add new directories to projects, components, or
nested within existing OSF directories. If `path` contains multiple
directory levels (e.g., `"data/rawdata"`) the intermediate-level
directories are created automatically. If the directory you're
attempting to create already exists on OSF it will be silently ignored
and included in the output.

## Usage

``` r
osf_mkdir(x, path, verbose = FALSE)
```

## Arguments

- x:

  One of the following:

  - An
    [`osf_tbl_node`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
    with a single OSF project or component.

  - An
    [`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
    containing a single directory.

- path:

  Name of the new directory or a path ending with the new directory.

- verbose:

  Logical, indicating whether to print informative messages about
  interactions with the OSF API (default `FALSE`).

## Value

An [`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
with one row containing the leaf directory specified in `path`.

## See also

Other OSF file operations:
[`osf_cp()`](https://docs.ropensci.org/osfr/reference/osf_cp.md),
[`osf_mv()`](https://docs.ropensci.org/osfr/reference/osf_mv.md),
[`osf_rm()`](https://docs.ropensci.org/osfr/reference/osf_rm.md)

## Examples

``` r
if (FALSE) { # \dontrun{
proj <- osf_create_project("Directory Example")

# add directory to the top-level of the Directory Example project
data_dir <- osf_mkdir(proj, path = "data")

# add a subdirectory nested within data/
osf_mkdir(data_dir, path = "rawdata")

# recursively create multiple directory levels within data/
osf_mkdir(data_dir, path = "samples/pcr/qc")
} # }
```
