# Open on OSF

View a project, component, file, or user profile on OSF with your
default web browser.

## Usage

``` r
osf_open(x)
```

## Arguments

- x:

  one of the following:

  - an OSF URL, or a generic string containing a GUID or Waterbutler ID.

  - an
    [`osf_tbl_node`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
    with a single project or component.

  - an
    [`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
    with a single file or directory.

  - an
    [`osf_tbl_user`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
    with a single OSF user.

## Examples

``` r
if (FALSE) { # \dontrun{
# Navigate to a project based on its GUID
osf_open("e81xl")

# You can also provide an osf_tbl subclass
crp_file <- osf_retrieve_file("ucpye")
osf_open(crp_file)
} # }
```
