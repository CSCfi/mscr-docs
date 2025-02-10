# Vocabulary Service
The Vocabulary Service collects and maintains common terminological vocubularies and concepts for community use. For example, researchers of a specific community can define concepts and their relationships using this service. Interested users can browse and check concepts and their definitions.

It was a late addition to the FAIRCORE4EOSC components ​and developed based on active code base from Finnish Interoperability platform ​which is developed by the Digital and Population Data Service Agency of Finland​.It was originally built for managing terminologiesbut this particular instance is deployed and customized by the FC4E project​

#### Main Features
- Graphical Interface to Create, maintain and publish vocabularies​.
- Support for SKOS-XL model​
- Separate status handling (VALID, DRAFT etc.) for vocabularies and concepts​
- Supports Import and export content using Excel​
- Linking within and between vocabularies​
- Resolvable PIDs for vocabularies and concepts​

## Vocabulary Service User Guide


### User Interface and Search Functions

In the vocabulary tool home page, a list of all the vocabularies in alphabetical order is visible.By clicking on the Vocabulary name in the list, User can view its contents,Metadata and possible actions. Users can also perform faceted searcg using the filtered search box found in the right side of the home page. It is possible to limit the search for vocabularies in the sidebars in the following ways:

![Alt text](../assets/voc-service-screenshots/home-page.png)

- With word search, User can search vocabularies and concepts, just like with the search in the top bar.
- If User only wants to see vocabularies created by a specific organization, select that organization from the drop-down menu.
- User can also choose which status he/she wants to see the Vocabularies in in the list. The options are: Valid, Draft, Superseded, Deactivated.
- User can also choose which knowledge areas for the Vocabularies in the list.

User can also search for vocubularies and concepts by typing the desired search term in the search field in the top bar. Then press enter key or the magnifying glass icon next to the search field.

![Alt text](../assets/voc-service-screenshots/search-bar.png)

### Adding vocabulary

![Alt text](../assets/voc-service-screenshots/create-new-voc.png)

User can add a new vocabulary clicking the "Add new vocabulary" button on the tool's home page. This will open up the modal where user need to put name and description(optional) and organization selector to create a new vocabulary. The created vocabulary will have draft PID and some metadata associated with and will get status Draft.

Clicking the create button, user will be navigated to detail page after successful creation of vocubulary.

### Vocabulary Detail Page
Vocabulary detail page consists of vocabulary metadata and different actions like adding concepts or downloading or uploading concept for that vocabulary. The user needs to have editing right to be able to see all the allowed actions related to a vocabulary.

![Alt text](../assets/voc-service-screenshots/voc-detail.png)

Clicking the small down arrow icon in the vocabulary information and actions window will show the possible actions and details of the vocabulary. 

### Editing Vocabulary and Concept Information

If user have the permission to edit, you can edit vocabulary metadata or can upload or add cocepts for the vocabulary. The various actions which are available are:

![Alt text](../assets/voc-service-screenshots/voc-actions.png)

#### Vocabulary actions
- Edit vocabulary
- Update vocabulary with a file
- Create new version of vocabulary
- Remove vocabulary 

![Alt text](../assets/voc-service-screenshots/concept-actions.png)
#### Concept related actions
- Add new concept
- Import concepts
- Add new collection
- Change statuses of the cocepts

You can also download the created vocabulary as a file with Download vocabulary action.


### Cocepts and Terms Home Page
![Alt text](../assets/voc-service-screenshots/add-concept.png)
### Importing Vocubularies and Concepts using Files
![Alt text](../assets/voc-service-screenshots/import-concepts.png)


