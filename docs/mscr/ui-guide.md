
## Login
To be able to create and register contents in MSCR, user needs to login with proper credentials. MSCR uses EOSC AAI and currently supports Google and Orcid as means of authentication. The current test version of MSCR deployment can be found at [MSCR Web App](https://mscr-release.2.rahtiapp.fi/).



## MSCR Home
After login, user should be able to see user's own workspace and the groups those which the user is part of. Both personal workspace is again divided in two main page- schemas and crosswalks. Schema page contains the schemas the user or his group have registered in MSCR and same for the crosswalks.

![Schemas in personal workspace](../assets/mscr-home-new.png)

## Contents in MSCR
The MSCR contents can be divided into two main categories. They are, Metadata Schemas and Crosswalk(See [MSCR Concepts](mscr/functional-overview.md)).The features that MSCR provides to manage the contents are mainly registering those contents in MSCR and different functionlities to manage them. 

## Content Registration 
### Schema Registration
Users can register their schemas of different formats in the MSCR and it will be stored with a resolvable handle in MSCR server. These handles can be used to reference the schema stored in MSCR. User can register schema either using an URI of already published schema elsewhere or uploading a schema file to MSCR Registry.

![Schema registering modal](../assets/register-schema.png)

The steps to add a schema in MSCR are as follows:

- Provide an URI or upload a schema file
- Select the file format for the intended schema.
- Add Name and Description (optional) for the schema.
- Add status (Default status should be DRAFT for the registered contents)
- Click Register button to continue.


##### Schema Registration with File Modal
![Schema registering with file](../assets/mscr/register-schema-with-file.png)

##### Schema Registration with URL Modal
![Schema registering with URL](../assets/mscr/register-schema-with-url.png)

If the schema registration goes successfully, the user will be navigated to schema metadata tab where all the metadata related to the regsistered schema is shown.

### General Error Situations while registering a schema
If the schema registration is unsuccessful, user will be prompted with the error message. The main issues currently for a failure to register the schema can be one of the following:

 - Unsupported File Format.
 - Parsing Error.
 - Missing field in the Form.

### Registering Crosswalks

Users can register their existing crosswalks with MSCR and can view the crosswalk in crosswalk editor if the crosswalk format is supported by MSCR. For registering a crosswalk follow the following steps:

- Select the source schema and target schema from the dropdown list. Remember, source and target schemas also need to be registered with MSCR and the visibility should be public before registering the crosswalk.
- Add the crosswalk file in the MSCR supported formats. See more in the supported formats link.
- Add name and description for the crosswalk.
- Draft state should be selected while registering new content.

![Crosswalk registration modal](../assets/register_crosswalk.png)

 

## Schema Management in MSCR

The basic functionalities that is available for schema management are

* Registering own Schemas or schemas hosted elsewhere by URL as draft.
* Visulizing the Schema with a schema tree (exception PDF schemas)
* Creating revisions of Schema
* Creating MSCR Copy of the Schema
* Deleting the Schema
* Publishing the schema.
* Type Editing for the schema properties

How these functions can be done in UI, is described below:




### Schema Detail View
If you click on the registered schema from the schema list, it will navigate to schema metadata and visualization view. This view has three tabs containing schema metadata, schema visualization and schema version history.

#### Schema Metadata 
You can see the schema specific details and the related files in the schema metadata view. If the user has the correct rights, schema metadata is editable and changes will be saved.

![Schema metadata tab view](../assets/schema-metadata.png)

To edit the schema metadata, one needs to select "edit metadata" from the schema action menu. After clicking it, fields of schema metadata will become and editable and changes need to be saved for the edit to be successful.

![Edit Schema metadata](../assets/edit-metadata-schema.png)


#### Schema Visualization
Schema visualization tab offers a tree view structure for the registered schema. Schemas are converted to an MSCR specific format and tree view is generated from that. The view may be empty for certain formats like PDF that cannot be rendered as a tree.

![Schema visualization tab view](../assets/schema-visualization.png)

#### Schema Version History
MSCR allows users to create and store different versions and variants for registered schemas. Schema version history tab consists of all the available versions for that specific schema.

![Schema version history tab view](../assets/version-history.png)

### Action Menu for Schema Visulization Tab

![Schema Action Menu](../assets/action-menu.png)

The basic actions available for the schema manipulation in the current MSCR UI are:

* Edit Metadata
    - Edit the metadata of the schema.

* Invalidate schema

* Deprecate schema
    - Means there is new version available for the specific schema which is preferred
* Add new revision
* Make MSCR Copy

### Creating MSCR Copy of a Schema
![Creating MSCR Copy of Schema](../assets/mscr-copy.png)
mkdocs
User can create a MSCR copy of the registered schema which transform the schema into internal format used in MSCR. This is a prerequisite for schema editing. This option is available when schema format is something that is possible to process to MSCR's internal format, whih are currently CSV, XSD, JSONSCHEMA, SHACL. State of the new copy will be always "Draft" and format will be "MSCR".

Creating MSCR copy is not available for schemas which are already in "MSCR" format.

### Creating a new revision of Schema

![Creating Revision of Schema](../assets/register-revision.png)

It is possible to create a new revision for the registered mscr schemas. The need for creating revisions can be that user wants to do some corrections or bug fixes to some already published content. The steps are almost like registering a new schema with some differences.

- User need to provide the schema file either as normal file upload or the URL
- Format and State of the content cannot be edited while creating a revision. So, revisions of the schema should be if the same format as the main content.
- Some meaningful name and description will help the user to find it easily later.


### Crosswalk Editor
MSCR offers a Crosswalk Editor where users can create mappings from the source schema to target schema and can export the generated mappings in MSCR supported formats.

- Select the source and target schema. Again, schemas should be registered and public in MSCR. When creating a new crosswalk, only schemas that can be rendered as trees are available.
- Add Name and Description(optional) for the Crosswalk. 
- Click Create Crosswalk button will lead to Crosswalk Editor Page.

 ![Crosswalk creation modal](../assets/create_crosswalk-1.png)
 

#### Creating New Crosswalk
Crosswalk editor is used to create mappings between schema fields which can be saved as new crosswalk. MSCR Crosswalk Editor offers a treeview of the selected source and target schemas where user can map the attributes between schemas and the mappings will be saved. 

![Crosswalk editor view](../assets/crosswalk editor.png)

- To start creating mappings, please click the action menu on the top right corner of the editor window and select edit.
![Finding Edit button by activating Actions button](../assets/edit_crosswalk.png)


 - After that, user can select attributes from two schemas present in left and right tree view and after selecting attributes to map, the mapping button between the two schema trees will be enabled.
![Button to link selected nodes](../assets/create_mapping.png)


- After clicking the mapping icon, pop up dialog will be opened where user can add some more details about the mapping. When it is done, Save button should be clicked to save the mapping. 
![Modal for editing mapping](../assets/edit_mapping.png)


- After saving, list of mappings will appear in a different tab
![List of mappings](../assets/mapping_list.png)






### Search Content

