# Extract OSF identifiers

Extract OSF GUIDs and Waterbutler IDs from various types of inputs.
Valid looking IDs are returned as `osf_id` objects.

## Usage

``` r
as_id(x)
```

## Arguments

- x:

  An `osf_tbl`, OSF URL, or a generic string containing a GUID or
  Waterbutler ID.

## Value

A character vector with class `osf_id`.

## Identifier types

There are 2 types of identifiers you'll encounter on OSF. The first is
the globally unique identifier, or GUID, that OSF assigns to every
entity. A valid OSF GUID consists of 5 alphanumeric characters. The
second type of identifier is specific to files stored on OSF. All file
operations on OSF are handled via Waterbutler. A valid Waterbutler ID
consists of 24 alphanumeric characters.

## Examples

``` r
if (FALSE) { # \dontrun{
# extract a GUID from an OSF URL
proj_id <- as_id("https://osf.io/7zqxp/")

# extract waterbutler IDs from an `osf_tbl_file`` with multiple files
osf_retrieve_node(proj_id) %>%
  osf_ls_files() %>%
  as_id()
} # }
```
