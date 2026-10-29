# OSF Tibbles

Items retrieved from OSF are represented as `osf_tbl` objects,
specialized data frames based on the
[tibble](https://tibble.tidyverse.org/reference/tibble-package.html)
class. See below for additional details.

## Details

Each row of an `osf_tbl` represents a single OSF entity. This could be a
user, project, component, directory, or file. An `osf_tbl` must include
the following 3 columns:

1.  `name`: indicates the name or title of the entity.

2.  `id`: the unique identifier assigned by OSF.

3.  `meta`: a list-column that stores the processed response returned by
    OSF's API. See the *Meta column* section below for more information.

## Subclasses

`osf_tbl` is the parent class of 3 subclasses that are used to represent
each of OSF's main entities:

1.  `osf_tbl_user` for users.

2.  `osf_tbl_file` for files and directories.

3.  `osf_tbl_node` for projects and components.

## OSF nodes

Projects and components are both implemented as *nodes* on OSF. The only
distinction between the two is that a project is a top-level node, and a
component must have a parent node (i.e., must be a sub-component of
another project or component). Because projects and components are
functionally identical, osfr uses the same `osf_tbl_node` class to
represent both.

## Meta column

The `meta` column contains all of the information returned from OSF's
API for a single entity, structured as a named list with 3 elements:

1.  `attributes` contains metadata about the entity (e.g., names,
    descriptions, tags, etc).

2.  `links` contains urls to API endpoints with alternative
    representations of the entity or actions that may be performed on
    the entity.

3.  `relationships` contains URLs to other entities with relationships
    to the entity (e.g., collaborators attached to a project).

This information is critical for `osfr`'s internal functions and should
not be altered by users. For even more information about these elements,
see [OSF's API
documentation](https://developer.osf.io/#tag/Entities-and-Entity-Collections).

## Acknowledgments

Our implementation of the `osf_tbl` class is based on `dribble` objects
from the [googledrive](https://googledrive.tidyverse.org) package.
