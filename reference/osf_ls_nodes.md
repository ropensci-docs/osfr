# List projects or components on OSF

List the projects or components associated with a user or contained in
the top-level of another OSF project or component.

## Usage

``` r
osf_ls_nodes(x, pattern = NULL, n_max = 10, verbose = FALSE)
```

## Arguments

- x:

  one of the following:

  - An
    [`osf_tbl_node`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
    with a single project or component.

  - An
    [`osf_tbl_user`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
    with a single OSF user.

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

An [`osf_tbl_node`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
with one row for each OSF project or component, ordered by modification
time.

## See also

[`osf_ls_files()`](https://docs.ropensci.org/osfr/reference/osf_ls_files.md)
to generate a list of files and files.

## Examples

``` r
if (FALSE) { # \dontrun{
# List your recent projects and components
osf_retrieve_user("me") %>%
  osf_ls_nodes()

# List the first 10 components in the #ScanAllFish project
fish_ctscans <- osf_retrieve_node("ecmz4")
osf_ls_nodes(fish_ctscans)

# Now just the components with scans of species from the Sphyrna genus
osf_ls_nodes(fish_ctscans, pattern = "Sphyrna")
} # }
```
