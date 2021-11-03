---
title: Schemas
has_children: true
nav_order: 1
---

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

# Schema structure

TODO: Add a nice navigable diagram here

## Required & Preferred Properties

Any properties in the schema that are required are specified in a `required` block. Every schema should have the `submitter_id`, `type` and any parental links listed as required attributes. Any submission of a particular node type that does not contain values for the required nodes will not pass validation.

Example from `study.yaml`:

```
required:
  - submitter_id
  - type
  - study_description
  - projects
```

A block of `preferred` attributes may also be specified. This would indicate an important field but submission of nodes without this field will still pass validation.

Example from `demographic.yaml`

```
preferred:
  - year_of_death
```

## Unique Keys

A set of `uniqueKeys` must be specified. This provides a way of uniquely identifying any node. 

note:
{: .label .label-yellow }

Am yet to come accross an example other than the one below. Not sure about the exact function of this field.

Example from `study.yaml`

```
uniqueKeys:
  - [id]
  - [project_id, submitter_id]
```

# References

* [Gen3 Data Dictionary documentation](https://gen3.org/resources/user/dictionary/)
* [Gen3 Data Dictionary repo](https://github.com/uc-cdis/datadictionary)
* [Gen3 Data Modelling webinar slides](https://gen3.org/community/webinars/Webinar_20190509.pdf)
