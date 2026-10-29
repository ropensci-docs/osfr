# Delete an entity from OSF

Use `osf_rm()` to **permanently** delete a project, component, file or
directory from OSF, including any uploaded files, wiki content, or
comments contained therein. Because this process is **irreversible**,
osfr will first open the item in your web browser so you can verify what
is about to be deleted before proceeding.

If the project or component targeted for deletion contains
sub-components, those must be deleted first. Setting `recurse = TRUE`
will attempt to remove the hierarchy of sub-components before deleting
the top-level entity.

*Note: This functionality is limited to contributors with admin-level
permissions.*

## Usage

``` r
osf_rm(x, recurse = FALSE, verbose = FALSE, check = TRUE)
```

## Arguments

- x:

  One of the following:

  - An
    [`osf_tbl_node`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
    with a single OSF project or component.

  - An
    [`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
    containing a single directory or file.

- recurse:

  Remove all sub-components before deleting the top-level entity. This
  only applies when deleting projects or components.

- verbose:

  Logical, indicating whether to print informative messages about
  interactions with the OSF API (default `FALSE`).

- check:

  If `FALSE` deletion will proceed without opening the item or
  requesting verification—this effectively removes your safety net.

## Value

Invisibly returns `TRUE` if deletion was successful.

## See also

Other OSF file operations:
[`osf_cp()`](https://docs.ropensci.org/osfr/reference/osf_cp.md),
[`osf_mkdir()`](https://docs.ropensci.org/osfr/reference/osf_mkdir.md),
[`osf_mv()`](https://docs.ropensci.org/osfr/reference/osf_mv.md)

## Examples

``` r
if (FALSE) { # \dontrun{
project <- osf_create_project("My Short-Lived Project")
osf_rm(project)
} # }
```
