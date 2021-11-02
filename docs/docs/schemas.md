---
title: Gen3 Schemas
has_children: true
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
| category             | The category of the schema, these are configurable                                               | in UMCCR dictionary they are: administrative, index_file, biospecimen, clinical, notation, data_file |
| program              | ? guess is that it can configure which program this schema could be a part of with * meaning all | '*'                                                                                                  |
| project              | ? guess is that it can configure which project this schema could be a part of with * meaning all | '*'                                                                                                  |
| description          | A description for the schema                                                                     | string                                                                                               |
| additionalProperties | Disallows a user from adding more properties than are specified in the schema when validating    | false                                                                                                |
| submittable          | Whether this schema is directly submittable to the gen3 portal                                   | true/false                                                                                           |
| validators           | ?                                                                                                | ?                                                                                                    |

## Links




# References

* [Gen3 Data Dictionary documentation](https://gen3.org/resources/user/dictionary/)
* [Gen3 Data Dictionary repo](https://github.com/uc-cdis/datadictionary)
* [Gen3 Data Modelling webinar slides](https://gen3.org/community/webinars/Webinar_20190509.pdf)
