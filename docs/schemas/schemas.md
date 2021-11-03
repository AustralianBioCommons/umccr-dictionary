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

## Required & Preferred Attributes

Any fields in the schema that are required are specified in a `required` block. Every schema should have the `submitter_id`, `type` and any parental links listed as required attributes. Any submission of a particular node type that does not contain values for the required nodes will not pass validation.

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

## Properties

Properties define the rules about the different 'fields' of the node, i.e. what kind of metadata will be stored against each node.

Each node should have:
 - property name
 - `description` - detailed description of the field
 - `type` - any of the existing [json schema](https://cswr.github.io/JsonSchema/spec/basic_types/) types

### Shared Property Definitions

In addition to the properties that you define as unique to a particular node, it is also useful to refer to properties that may be shared across many nodes. These properties can be saved within the `_definitions.yaml` and referred to as needed.

Some examples from the gdc dictionary are:

#### Ubiquitous properties 

This `_definitions.yaml#/ubiquitous_properties` contains many of the required system properties such as `submitter_id` and `state`

#### Link properties

These are referred to by the property that describes the link and reflect the multiplicity of the link.

### Property Types

Most property types are straight forward. Some of the types are explained in further detail below.

### Numeric properties

Properties with a numeric type, that is `integer` or `number` can be restricted with minimum and maximum values.

Example from `diagnosis.yaml`

```
age_at_diagnosis:
    description: Age at the time of diagnosis expressed in number of days since birth.
      If the age is greater than 32872 days (89 years), see 'age_at_diagnosis_gt89'.
    type: integer
    maximum: 32872
    minimum: 0
```

### String properties

#### Patterns

#### Enumerations

#### Term definitions, vocabulary and ontologies

# References

* [Gen3 Data Dictionary documentation](https://gen3.org/resources/user/dictionary/)
* [Gen3 Data Dictionary repo](https://github.com/uc-cdis/datadictionary)
* [Gen3 Data Modelling webinar slides](https://gen3.org/community/webinars/Webinar_20190509.pdf)
