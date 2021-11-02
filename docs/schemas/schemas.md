---
title: Gen3 Schemas
has_children: false
nav_order: 2
---

# Introduction

# Schema structure



## Descriptors

| Key                  | Description                                                                                      | allowed values                                                                                       |
|----------------------|--------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| $schema              | The version of json schema                                                                       | "http://json-schema.org/draft-04/schema#"                                                            |
| id                   | Node id used for data query/submission                                                           | string                                                                                               |
| title                | Name for the schema                                                                              | string                                                                                               |
| type                 | The type of the schema                                                                           | 'object'                                                                                             |
| namespace            | the commons that uses this schema, usually a url                                                 | string                                                                                               |
| category             | categories that represent broad roles for the node, these are customisable for different data models. Useful in querying as you can select all nodes of a particular category | in UMCCR dictionary they are: administrative, index_file, biospecimen, clinical, notation, data_file |
| program              | ? guess is that it can configure which program this schema could be a part of with * meaning all | '*'                                                                                                  |
| project              | ? guess is that it can configure which project this schema could be a part of with * meaning all | '*'                                                                                                  |
| description          | A description for the schema                                                                     | string                                                                                               |
| additionalProperties | Disallows a user from adding more properties than are specified in the schema when validating    | false                                                                                                |
| submittable          | Whether this schema is directly submittable to the gen3 portal | true/false                                                                                           |
| validators           | ?                                                                                                | ?                                                                                                    |
| systemProperties     | these properties are those that will be automatically filled by the system unless otherwise defined by the user. These basic properties define the node itself but still need to be placed into the model. | as a minimum <br> - id <br> - project_id <br> - state <br> - created_datetime <br> - updated_datetime|

## Links

Links are what join the nodes of your data model together. The links go FROM the child TO the parent with the Program always being the ultimate root. Links are also described with a `backref`, `label` and `multiplicity` that should match up to one of the specified relationships in the `_definitions.yaml` file.


| Key          | Description                                                                                                         | example values                                                         |
|--------------|---------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| name         | The name of the link from this schema to its parent, usually the parent's name in plural form                       |                                                                        |
| backref      | The back reference from the parent back to the child, usually the name of the schema pluralised                     |                                                                        |
| label        | A descriptor for the type of relationship. (Not sure if this is a controlled vocabulary or free text)               | describes, member_of, derived_from, data_from                          |
| target_type  | the node id of the parent                                                                                           |                                                                        |
| multiplicity | describes the numeric relationship from the child to the parent, these should be defined in the `_definitions.yaml` | one_to_one, one_to_many, many_to_many, to_one_project, to_many_project |
| required     | Whether each instance of this schema needs to have this link                                                        | `true`, `false`                                                        |

example links code from gdc dictionary `case.yaml`:

```
links:
  - name: experiments 
    backref: cases
    label: member_of
    target_type: experiment
    multiplicity: many_to_one
    required: true
```

The above `links` snippet is specifying that a `case` is a `member_of` an `experiment`, i.e. the `experiment` is the parent of the `case`. The `multiplicity` indicates it is a `many_to_one` relationship, that is, many cases can be a part of a single experiment. The `required` property indicates this relationship is required, that is, every case that is submitted must be linked to a single experiment.

If a child can link to multiple parents, that is, be a child of either `parentA` OR `parentB` , simply list an additional link, example from gdc dictionary `clinical_test.yaml`

```
links:
  - name: cases 
    backref: clinical_tests
    label: performed_for 
    target_type: case
    multiplicity: many_to_one
    required: true
  - name: diagnoses
    backref: clinical_tests
    label: relates_to
    target_type: diagnosis
    multiplicity: many_to_many
    required: false
```

If a single node instance needs to link to multiple parents, that is, be a child of both `parentA` AND `parentB`, it is necessary to specify a non-exclusive relationship, setting `exclusive` property to false and listing the two links under a `subgroup` property. 

Example from gdc dictionary `submitted_aligned_reads.yaml`

```
links:
  - exclusive: false
    required: true
    subgroup:
    - name: read_groups
      backref: submitted_aligned_reads_files # pretty ugly
      label: data_from
      target_type: read_group
      multiplicity: one_to_many
      required: false
    - name: core_metadata_collections
      backref: submitted_aligned_reads_files
      label: data_from
      target_type: core_metadata_collection
      multiplicity: many_to_many
      required: false
```



# References

* [Gen3 Data Dictionary documentation](https://gen3.org/resources/user/dictionary/)
* [Gen3 Data Dictionary repo](https://github.com/uc-cdis/datadictionary)
* [Gen3 Data Modelling webinar slides](https://gen3.org/community/webinars/Webinar_20190509.pdf)