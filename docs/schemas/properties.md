---
title: Properties
has_children: false
parent: Schemas
nav_order: 3
---

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