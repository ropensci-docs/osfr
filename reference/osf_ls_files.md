# List files and directories on OSF

List the files and directories in the top-level of an OSF project,
component, or directory. Specify a `path` to list the contents of a
particular subdirectory.

## Usage

``` r
osf_ls_files(
  x,
  path = NULL,
  type = "any",
  pattern = NULL,
  n_max = 10,
  verbose = FALSE
)
```

## Arguments

- x:

  One of the following:

  - An
    [`osf_tbl_node`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
    with a single project or component.

  - An
    [`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
    with a single directory.

- path:

  List files within the specified subdirectory path.

- type:

  Filter query by type. Set to `"file"` to list only files, or
  `"folder"`to list only folders

- pattern:

  Character string used to filter for results that contain the substring
  `"pattern"` in their name. *Note:* this is a fixed, case-insensitive
  search.

- n_max:

  Maximum number of results to return from OSF (default is 10). Set to
  `Inf` to return *all* results.

- verbose:

  Logical, indicating whether to print informative messages about
  interactions with the OSF API (default `FALSE`).

## Value

An [`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
with one row for each file or directory, ordered by modification time.

## See also

[`osf_ls_nodes()`](https://docs.ropensci.org/osfr/reference/osf_ls_nodes.md)
to generate a list of projects and components.

## Examples

``` r
if (FALSE) { # \dontrun{
# Retrieve the Psychology Reproducibility Project from OSF
psych_rp <- osf_retrieve_node("ezum7")

# List all files and directories
osf_ls_files(psych_rp)

# ...only the directories
osf_ls_files(psych_rp, type = "folder")

# ...only PDF files
osf_ls_files(psych_rp, type = "file", pattern = "pdf")

# List the contents of the first directory
osf_ls_files(psych_rp, path = "RPP_SI_Figures")
} # }
```
