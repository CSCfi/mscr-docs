# Release notes


#### 0.5.0-beta December 5, 2023

- Authentication using EOSC AAI
- Registering and Uploading MetaData Schemas in XML, JSON, XSD and PDF Formats.
- Registring Crosswalks in JSON, PDF and XSLT formats.
- Search and browse for registered schemas and crosswalks.
- Initial version of Croswalk editor with simple mapping.

#### 0.5.1 February 21, 2024
- Restrict schema formats (current supported formats are JSON, CSV and SKOSRDF) for crosswalk creation.
- Implemented responsive MUI grid to metadata and files and added Action menu.
- Implemented Crosswalk version info view.
- Minor bug fixes and UI Style Updates.
- Updated Group Management application where users can create API tokens.

#### 0.5.2 March 5, 2024
- Uniform view for schema and crosswalk metadata and files tabs.
- Editing schema metadata.
- Removed language selector from content creation dialogs. Deafult language is english.
- Downloading files from schema and crosswalk metadata tab.
- RDFS and SHACL format support for crosswalk creation.
- Minor bug fixes and UI updates.

#### 0.5.3 March 19, 2024
- Added resolvable handle PIDs for MSCR Contents.
- Added endpoint for exporting vocabulary as JSON Schema enum.
- Add SKOS export to crosswalks that are between vocabularies.
- Added Tree Visualization for schemas.
- Schema Deletion: Schemas can be deleted if they are in Draft state.
- Improved content creation and editing rights managements for group workspace.
- Minor bug fixes and UI improvements

#### 0.5.4 May 21, 2024
- Added Content Versioning and navigations to different versions.
- Clear Error messages while registering schemas.
- Added new states for registered contents(Invalid, Deprecated).
- UI Improvements and minor bug fixes.

#### 0.5.5 June 18, 2024
- Added loading indicator when schema tree is being loaded
- Added option to hide navigation panel
- Minor bug fixes

#### 0.5.6 July 2, 2024
- Added Action menu option to make MSCR copy of a schema (original schema format must be MSCR, JSON, CSV, SHACL or XSD; resulting schema format is MSCR)
- Minor bug fixes
