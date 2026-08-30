# Retrieve an entity from OSF

Create an
[`osf_tbl`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
representation of an existing OSF project, component, file, or user
based on the associated unique identifier. Usually this is a 5-character
global unique identifier (GUID) but for files or directories, it could
also be an 11-character Waterbutler ID. See below for details.

## Usage

``` r
osf_retrieve_user(id)

osf_retrieve_node(id)

osf_retrieve_file(id)
```

## Arguments

- id:

  An OSF identifier corresponding to an OSF user, project, component, or
  file. Set `id = "me"` to retrieve your own OSF profile.

## Value

An
[`osf_tbl_user`](https://docs.ropensci.org/osfr/reference/osf_tbl.md),
[`osf_tbl_node`](https://docs.ropensci.org/osfr/reference/osf_tbl.md),
or [`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
containing the corresponding OSF entity.

## OSF identifiers

A 5-character GUID is assigned to every user, project, component, and
file on OSF and forms the basis for the service's URL scheme. For
example the GUID for a project accessible at <https://osf.io/ezum7> is
simply `ezum7`. You can learn more about GUIDs in the [OSF
FAQ](https://help.osf.io/article/203-faqs).

An important detail is that files and directories are handled internally
on OSF by another serviced called
[Waterbutler](http://www.waterbutler.io/), which uses 11-character
identifiers. Although Waterbutler IDs are largely hidden from users on
<https://osf.io>, they represent the primary method for identifying
files/directories by the OSF API. In fact, files do not receive a GUID
until it is viewed directly on <https://osf.io> and directories never
receive a GUID. Therefore, osfr relies on Waterbutler IDs for files and
directories, and always includes them (rather than GUIDs) in
[`osf_tbl_file`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
objects.

## Retrieving OSF objects

To begin using osfr to interact with resources on OSF you must use one
of the following *retrieve* functions to create an
[`osf_tbl`](https://docs.ropensci.org/osfr/reference/osf_tbl.md) that
contains the entity of interest. Note the functions are entity-type
specific, use:

- `osf_retrieve_node()` to retrieve a project or component

- `osf_retrieve_file()` to retrieve a file or directory

- `osf_retrieve_user()` to retrieve a user

## A note on 3rd-party storage providers

While OSF supports integration with a variety of 3rd-party cloud storage
providers, osfr can currently only access files stored on the default
OSF storage service. Support for additional storage providers is planned
for a future release.

## Examples

``` r
if (FALSE) { # \dontrun{
 # retrieve your own OSF user profile (must be authenticated, ?osf_auth)
 osf_retrieve_user("me")

# retrieve the Psychology Reproducibility Project (P:RP, osf.io/ezum7)
osf_retrieve_node("ezum7")

# get the first figure from the P:RP
osf_retrieve_file("https://osf.io/7js8c")
} # }
```
