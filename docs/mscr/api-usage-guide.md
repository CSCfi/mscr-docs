This document describes the functionality of the MSCR API with concrete examples. 

Prerequisites:

* API key for the MSCR API (See [Getting Started](mscr-api-getting-started.md))
* curl or similar tool for send HTTP request.

# Registering content

MSCR works as a registry for schemas and crosswalks (later referred to as content). 

## Schemas

Registering schemas is the prerequisite for registering crosswalk. The reason for this is that regardless of the type or format of the crosswalk the metadata of the registered crosswalk must always contain a MSCR controlled PID for both source and target schema. In other words, in order to create a crosswalk between schema X and schema Y, they both need to be first registered to the MSCR. 

### Add PDF schema

PDF schemas are human readable documentation how the data should look like. They can registered in the same way as any other schema format, but they cannot be used as source or target schema in the crosswalk editor. However, PDF type schemas can be referenced by other types of crosswalks, such as XLST. 

**Task:**

Register a PDF description of a schema. This content has not been published anywhere else what MSCR will be the service that also hosts the content. When the PID of the content is resolved, it should point to the MSCR. The schema must be registered as part of user's personal content i.e. it should not have any relationship to an organization.

**Steps:**

* Get the file. Demo PDF file can be downloaded [here](../data/dummy.pdf).

* Create schema metadata as JSON
    ```json 

    {
        "state": "PUBLISHED",
        "visibility": "PUBLIC",
        "namespace": "http://example.com/myschema",
        "versionLabel": "v1.0.0",
        "label": {
            "en": "My schema"
        },
        "description": {
            "en": "This is myschema."
        },
        "languages": [
            "en"
        ],
        "organizations": [],
        "format": "PDF"
    }
    ```

    Organization property is left empty, because the owner of the content is the current user. See separate documentation for details of the metadata fields. 

* Send the data to the API. We are using and endpoint (`https://mscr-test.rahtiapp.fi/datamodel-api/v2/schemaFull`) that allows for both metadata and content to be uploaded at the same time. This endpoint requires data to be sent as form data. There must be two forms fields: metadata and file.     
    ```bash 
    curl  -X PUT \
  'https://mscr-test.rahtiapp.fi/datamodel-api/v2/schemaFull' \
  --header 'Authorization: Bearer <REPLACE WITH API TOKEN>' \
  --form 'metadata="<REPLACE WITH JSON STRING OF THE METADATA>"' \
  --form 'file=@<REPLACE WITH PATH TO FILE>'
    ```

### Add JSON Schema

Schemas can be added as JSON Schema documents. You cannot just add any JSON file, but the file has to be compliant with specific supported versions of the JSON schema specification. The specification must also be indicated in the file by $schema property in the root object. 

Support JSON schema specifications:
* draft-04 (http://json-schema.org/draft-04/schema#)

**Task**

Add a draft JSON schema to registry just for testing. The schema should be registered under the personal data of the user. After adding the first file, replace the file with new version without creating a new schema. Lastly, we update the metadata of the schema by setting a new version label. 

**Steps**

* Prepare the schema document. Sample schema can be found [here](../data/test_schema.json).
    ```json

    {
    "$schema" : "http://json-schema.org/draft-04/schema#",
    "description" : "simple schema with one object.",
    "type" : "object",
    "properties" : {
        "firstName" : {
        "type" : "string"
        },
        "lastName" : {
        "type" : "string"
        },
        "address" : {
            "type" : "object",
            "title" : "Address of the person",
            "properties" : {
                "street" : {
                "type" : "string"
                },
                "house_number" : {
                "type" : "string"
                },
                "city" : {
                    "type" : "object",
                    "properties" : {
                        "population" : {
                        "type" : "integer"
                        }
                    }
                }
            }
        }
    },
    "additionalProperties" : false
    }
    ```
    The sample schema contains three properties at the root, two of type string and one of object object. Object type properties can contain their own properties. Each property should have "type" and "title" information. If type is missing, the default type "string" is used. Title information is used and the name of property if available, otherwise the value of the key (e.g. "house_number") is used as the name. 

* Create schema metadata as JSON
    ```json

    {
        "state": "DRAFT",
        "visibility": "PRIVATE",
        "namespace": "http://example.com/test1",
        "versionLabel": "just testing",
        "label": {
            "en": "First test"
        },
        "description": {
            "en": ""
        },
        "languages": [
            "en"
        ],
        "organizations": [],
        "format": "JSONSCHEMA"
    }
    ```

    Visibility field can used to exclude content from the search index, but only content in DRAFT state and be hidden from the search. You can try to change state to "PUBLISHED" and see what happens.

* Register new schema with first version of the JSON schema
    ```bash

    curl  -X PUT \
    'https://mscr-test.rahtiapp.fi/datamodel-api/v2/schemaFull' \
    --header 'Authorization: Bearer <REPLACE WITH API TOKEN>' \
    --form 'metadata="<REPLACE WITH JSON STRING OF THE METADATA>"' \
    --form 'file=@<REPLACE WITH PATH TO FILE>'

    ```

* Prepare the next version of the JSON Schema file.

    In this scenario, we don't want to register a new schema, but just to replace the content of the schema by uploading a new file to already registered schema. This can be done for content that is in DRAFT state. In other states, it is not possible to change the content of the schema with out creating a whole new schema (with a new PID). 
    
    Modified sample schema can be found [here](../data/test_schema.json). The only change is that we wanted to have a nicer title for the house_number property. 

    ```json

    {
        "$schema" : "http://json-schema.org/draft-04/schema#",
        "description" : "simple schema with one object.",
        "type" : "object",
        "properties" : {
            "firstName" : {
            "type" : "string"
            },
            "lastName" : {
            "type" : "string"
            },
            "address" : {
                "type" : "object",
                "title" : "Address of the person",
                "properties" : {
                    "street" : {
                    "type" : "string"
                    },
                    "house_number" : {
                    "type" : "string",
                    "title": "House number"
                    },
                    "city" : {
                        "type" : "object",
                        "properties" : {
                            "population" : {
                            "type" : "integer"
                            }
                        }
                    }
                }
            }
        },
        "additionalProperties" : false
    }
    ```

* Replace schema content with a new file.

    In order to replace the content of an existing schema, one has to use the `https://mscr-test.rahtiapp.fi/datamodel-api/v2/schema/<pid>/upload` endpoint. The `<pid>` must be replace by the PID of the schema that is to be updated. This operation is only allowed for content in the DRAFT state. 

    ```bash
    curl  -X PUT \
  'https://mscr-test.rahtiapp.fi/datamodel-api/v2/schema/<REPLACE WITH THE PID OF THE SCHEMA>/upload' \
  --header 'Authorization: Bearer <REPLACE WITH API TOKEN>' \
  --form 'file=@<REPLACE WITH PATH TO FILE>'
    ```

* Prepare updated metadata

    We want to change the value of the "versionLabel" property. 
    ```json
    {
        "versionLabel": "just testing (v2)"
    }    
    ```

* Update schema metadata.

    The metadata of a content can changed at any point regardless of the state of the content. Metadata can be update by sending a POST (as opposed to PUT when creating content) to endpoint `https://mscr-test.rahtiapp.fi/datamodel-api/v2/schema/<PID>`, where `<PID>` is the identifier of the content. The content or body of the request should contain the metadata field that need to be changed. 

    ```bash
    curl  -X POST \
    'https://mscr-test.rahtiapp.fi/datamodel-api/v2/schema/<REPLACE WITH THE PID OF THE SCHEMA>' \
    --header 'Authorization: Bearer <REPLACE WITH API TOKEN>' \
    --header 'Content-Type: application/json' \
    --data-raw '{
        "versionLabel": "just testing (v2)"
    }'    
    ```

### Publish a schema in DRAFT state

Published schema is considered to be stable in a sense that it should not change anymore. The visibility of a published schema is always "PUBLIC", meaning that is it accessible by anyone either through the search functionality of via direct link. This goes for both metadata and the content of the schema. When the state is changed from DRAFT to PUBLIC, it cannot be changed back to DRAFT anymore. 

**TODO**

### Add a new revision

Revision is a new version of a existing piece of content. Revisions of a content are all connected to one another through a shared internal identifier (aggregationKey). Even though each piece of content with a PID has its own set of metadata fields, all revisions of a content usually share the same of similar title. Version label property can be used for additional version information for each revision. Examples of version labels are for example "v.1.0.1" and "2022-10-10". 

A new revision is always created from the latest revision, meaning that no branches are allowed. 

``` mermaid
classDiagram
  URN2  <-- URN3:revisionOf
  URN1  <-- URN2:revisionOf
  class URN3{
    label "My Schema"
    versionLabel: "0.0.1"
    aggregrationKey: "URN1"
    state: PUBLISHED
  }
  class URN2{
    label "My Schema"
    versionLabel: "draft"
    aggregrationKey: "URN1"
    state: PUBLISHED
  }
  class URN1{
    label "My Schema"
    versionLabel: "draft"
    aggregrationKey: "URN1"
    state: DRAFT
  }    
```

Looking at the Figure 1, we can see that the latest revision of "My schema" is published, so we cannot change the content of the schema without creating a completely new schema. If we don't want to create another completely separated schema called "My schema", we can create a revision of the existing schema. 

**Task**

Create a new revision of a published schema. The metadata of the new version can have the same title as the old one, but version label must changed. 

**Steps**

```json
{
    "format": "PDF",
    "status": "DRAFT",
    "state": "DRAFT",
    "visibility": "PUBLIC",
    "versionLabel": "1",
    "label": {
        "en": "string"
    },
    "description": {
        "en": "string2"
    },
    "languages": [
        "en"
    ],
    "organizations": [
        "7d3a3c00-5a6b-489b-a3ed-63bb58c26a63"
    ],
    "sourceSchema": "urn:IAMNOTAPID:515d74db-5469-4814-b503-d2677317c5c1",
    "targetSchema": "urn:IAMNOTAPID:515d74db-5469-4814-b503-d2677317c5c1"
}
```