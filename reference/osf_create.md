# Create a new project or component on OSF

Use `osf_create_project()` to create a new top-level project on OSF. A
nested component can be created by providing an
[`osf_tbl_node`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
containing an existing project or component to
`osf_create_component()`'s `x` argument.

## Usage

``` r
osf_create_project(
  title,
  description = NULL,
  public = FALSE,
  category = "project"
)

osf_create_component(
  x,
  title,
  description = NULL,
  public = FALSE,
  category = NULL
)
```

## Arguments

- title, description:

  Set a title (required) and, optionally, a description.

- public:

  Logical, should it be publicly available (`TRUE`) or private (`FALSE`,
  the default)?

- category:

  Character string, specify a category to change the icon displayed on
  OSF. The defaults are `"project"` for projects and `"uncategorized"`
  for components. The specified category can be easily changed later on
  OSF. Valid category options include:

  - analysis

  - communication

  - data

  - hypothesis

  - instrumentation

  - methods and measures

  - procedure

  - project

  - software

  - other

- x:

  An
  [`osf_tbl_node`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
  with a single OSF project or component that will serve as the new
  sub-component's parent node.

## Value

An [`osf_tbl_node`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
containing the new project or component.

## OSF nodes

Projects and components are both implemented as *nodes* on OSF. The only
distinction between the two is that a project is a top-level node, and a
component must have a parent node (i.e., must be a sub-component of
another project or component). Because projects and components are
functionally identical, osfr uses the same
[`osf_tbl_node`](https://docs.ropensci.org/osfr/reference/osf_tbl.md)
class to represent both.

## References

1.  OSF Guides: Create a Project.
    <https://help.osf.io/article/383-creating-a-project>.

2.  OSF Guides: Create a Component.
    <https://help.osf.io/article/253-create-components>.

## Examples

``` r
if (FALSE) { # \dontrun{
# create a new public project
project <- osf_create_project(title = "Private OSF Project", public = TRUE)

# add a private component to the new project
component <- osf_create_component(project, title = "Project Data")
} # }
```
