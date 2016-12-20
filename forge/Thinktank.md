---
tags: Forge
---

Thinktank
=========

TAO X.X - Surveys Management and Advanced Item Bank Translation capabilities (Not yet released)
-----------------------------------------------------------------------------------------------

### 1. Dedicated authoring tool for surveys

\> Background questionnaire and survey management: template-based survey item authoring, and survey items repository.\
\> Design complete surveys including cognitive assessments and background data collection in a fully integrated way.\
\> Design Branching rules, consistency checks and derived variables in your questionnaire.

### 2. Translation capabilities with support for a professional translation outside TAO through XLIFF standard format.

\> Advanced functionalities for translation and context adaptation of test and items, including support for professional translators and standard translation tools\
\> Improve the quality of content translation, and cross-language comparability through translation and verification quality processes into TAO for multilingual surveys and assessments\
\>Translation Capabilities will be split into three different components and integrated within a new extension “lgItem” extending taoItem. This extension will include three actions to be declared inside the “structure.xml” file describing actions pertaining to a new extension.

\> 1. Xliff extractor relying on one item (either QTI or OWI) , proposing an interface requesting an optional xliff file, prompting for a target language, and generating an xliff file. If a translated xliff file is provided, the generated xliff file will include the translated translation units. (see christophe for this) The generated xliff file contains an identifier for the item (which is a versionned controlled content) thus including a uri and a version number.This action relies on the validation of content files (below).\
\> 2. Item Validation. This new action will validate items (any type) against different levels of checks. Syntaxical (QTI xsd, xHTML xsd) TAO (does the item include the TAO API) lgItem (are the content files valid for xliff generations)\
\> 3. Xliff Injection. Applies the provided xliff file into a selected Item. A user interface will prompt for a target language overwriting target language found from the xliff file. A check for the uri and the version number found in the xliff file will be eprformed against the current version of the selected item. Legacy Item types : C-TEST, requires further checks for xliff generation

### 3. Multilingual tests management

TAO 2.X Advanced Tests
----------------------

-   Simple Tests authoring. Currently, it is possible to design very easily very simple sequential tests and re-order items. It is possible to go further but exclusively through the advanced authoring tool and design complex branching rules or includes activities inside the test presenting web-based applications. This authoring tool not being dedicated on the testing problematic but on the general process and workflow problematic, it is rather complex to use. We need an easier way to design simple tests with branching rules. Branching rules are expressed using an expression relying on variables coming from executed items, other web-based activities of the tests or derived variables. This authoring tool should enable to define navigation policy (going forward/backward) on global level and on an item level. Other parameters like the layout, possibility to pause the test, to break it off, to position items inside the test and buttons positionning should be configurable from this interface.

<!-- -->

-   Internationalisation\
    Support for Right to left writing languages, get reliable fonts for test delivery, encoding, adapt formatting tools to cultural needs.

<!-- -->

-   Tests inclusion. In order, to enable the possibility to include and re-use existing tests inside new tests, we need to improve the process extensions and implement sub-process management. This involves to manage how variables are given as input to the sub-process and how they are output. At the level of the model, an activity needs to extend Process and get the definition of a process with all the information required.

<!-- -->

-   Item Bags and selection policy. Inside a test, we need to be able to design a section that will for example random a specific amount of items randomly from a determined bag of items. Such bags and selection algorithms (“select N randomly w/o re-selection”/ Adaptive algorithm / user deifned algorithm, needs to be implemented at the level of the process extension

\* Offline Tests. Offline Tests will be configured at the level of the delivery extension and will be implemented at the level of the tao runtime API. This API provides interface for :

1.  Time Line management (what are the next activities ? Go to the enxt activity ? Am I allowed to go backwards ?
2.  Item API (Store and exchange variables)
3.  Session Management (identify user, starts and ends a test session)\
    The online backend of tao consitutes an implementation of this API interface. We need to provide an offline implementation based on the local browser capacities (HTML5 db ?, javascript).

-   Multilingual test\
    Users should be able to create multilingual tests, where the user could toggle language during the test. Tis means that we may either create different tests, each of them being in a different language and assign them to different groups based on their mother tongue or create a multilingual test.

<!-- -->

-   Open Web Tests\
    Similarly to the way we opened the possiiblity at the level of items to play user defined items in a tao test thanks to the tao api. We should be able to play a user defined test. Different steps for this may be envisionned : 1. PLay a complet home made test, 2. Play a home made test that complies with tao api in order to upload results, 3. Play a home made test that rely on tao items.

<!-- -->

-   Add QTI meta-data Models

TAO 2.X R/Concerto Integration : Advanced Results, Reports management, Item eprsonnaliszation
---------------------------------------------------------------------------------------------

### 1. Reports extension (individual-grouped feedback-reports)\
\>Users may design reports and manage them (classify them and characterize them similarly to the way users may manage any other resources in TAO). When users design a report template they define the static content using an XHTML toolbar as used in Concerto v3 HTML templates. In addition to this static part, users may define placeholders in the template report, and assign them a variable reference directly into the report template. Using Concerto logic and by means of a graphical programming interface, they may express how to compute the data in order to populate the variable that will get substituted with the variable reference at the placeholder location. For this, while programming the logic they may rely on different sources of data which depends on the use case:

-   Individual feedback : In this scenario, the user gets a contextual test taker identification, he may directly query for the collected data arising from test execution (score, [endorsement, actual response] for each items), query for data describing the test taker arising from the test taker extension of TAO and in a more general way query for any data available from TAO (characteristics of items, etc.);
-   Grouped feedback : In this scenario, the user can retrieve the same type of information but the user needs to identify the scope of individual for whom to fetch the data.\
    In all cases, the user is provided with the statistical function provided by R.

### 2. Dynamic/Concerto Items

\>TAO provide different item types giving more or less freedom in terms of interaction types users may create. TAO currently manage three item types, QTI (all interactions arising from paper pen), OWI (complete freedom). This covers a broad range of item types. But the content of items remains strictly determined by means of the encoding made in the authoring tool An additional item type “Concerto item type” would allow to define dynamic items where the content or part of the content gets computed using R logic and relying on all data available from the knowledge base (data from test execution and/or any other resource). When users design an item template they define the static content using an XHTML toolbar as used in Concerto v3 HTML templates. In addition to this static part, users may define placeholders in the template report, and assign them a variable reference directly into the report template. Using Concerto logic and by means of a graphical programming interface, they may express how to compute the data in order to populate the variable that will get substituted with the variable reference at the placeholder location.

### 3. Item Calibration

Integration with Concerto and R open-source statistical platform\
Increase advanced testing capacity and access high level psychometric features with cutting-edge IRT and adaptive testing technology, integrate powerful data analysis capabilities into TAO for item calibration, result analysis, IRT scoring, etc… from free open-source companion tools

### 4. New Result management extension

-   Export data. Currenlty, you can design a table for data you are interested in and export it in CSV. This file contains all the data as strings (for every information like what was the selected answer , what was the school the student was in, from which department comes the employee was stored as an explicit litteral) . Statisticians are used to work with numerical values for analysis. An additionnal export could be split into two files one describing the semantics of every variables and possible values (the columns from the table of data) and their related numerical values, the other file containing all numerical values. This is analog to how SPSS work.

<!-- -->

-   Selection of properties to be added to the table of results (UTR)

There are restrictions at the level of properties selection of columns to populate tables. It is restricted to informations connected from the results, like the age of the studeing having passed the test related to the results but it is not possible to select informations defined the other way in the model like the teacher having the student who has taken the test.

-   Ergonomy of the table of results tool (UTR)\
    Based on the outcome from usability lab planned, a re-design of the suer interfaces will be performed.\
    Increased usability and flexibility to create result tables combining test results, item, test, group, subject, and delivery meta-data and background information using the improved table builder and meta-data explorer, connect result table with data analysis tools directly from TAO using the embedded R user interface.\
    In addition, the current user interfaces are not consistent with graphical widgets and layout used in the tao platform in general.

TAO 3.0 Open Item Bank (& Items / Extension MarketPlace)\
- Switch to NoSQL model (Virtuoso or similar)
---------------------------------------------------------

The architecture of tao allows for multiple backend implementation of the data storage. New backend requires to re-implement a proxy. This allows to interact with NoSQL database implementing probably Sparql queries adressing the the chosen noSQL database. A first experiment was already achieved using Virtuoso (only a few subset of all the api was implemented).

- Deployment of an online Open Item Bank\
- Collect copyleft items

-Deployment of an extension directory\
- MarketPlace

Miscellaneous
-------------

### Generic widget to select resources. (Planned for TAO 2.2)

TAO would benefit from advanced search facilities to help users when populating groups with the adequate subjects, or when selecting items constituting a test using criteria/property based search, facet based search, full text search. All those search facilities should come together with the tree view widget that is presented each time the user is invited to select explicitly resources.\
h3. Active Directories : LDAP support\
h3. Advanced models management.

There should be an additional pane in the TAO user interface to enable models edition relying on core functionnalities of Generis and perform advanced modifications on the ontology. Due to the taxonomy approach proposed in all tao extensions, it is currently not possible to describe other things that are not Subjects, groups, Tests, etc.

In terms of design, the meta-tao extension tao contains all graphical user interfaces libraries, while our extension “models” could benefit from those libraries. Ideally we would have externalised the libraires into generis core or helpers, keep the tao meta-extension holding the global model/Ontology describing TAOObjects. From such an architecture, we would build a new extension of generis providing user interfaces relying on the external graphical libraries.

### Transactions management / Inference management / rights access management

Generis on which rely TAO would benefit in terms of scalability and implementation from a prolog based core engine since such rule based features and transactions management are close to horn clauses that prolog already impelments natively. The RDF parser is distributed with SWI-Prolog under the LGPL Free Software licence.\
Hopefully the architecture of the backedn of generis is flexible and a new implementation of the generis API would fit into the architecture.

### Peer to peer network

TAO extensions (Subjects, Groups, etc.) could be distributed on a network of tao installations and exchange of informations between modules automatized to allow users for example to populate its tests using items from any item module available on the network. This feature was implemented in the former prototype but is not available yet in the new product.

Generalisation of the communication between generis installation should be achieved (based on any user defined relation in the ontology). Communciation between generis installation could be set up tahnks to subscription which could be disable and containing possibly triple mask to identify more precisely which other generis installation contains knowledge about what is being requested. Rights access management will restrict acces to the knowledge base.

This feature would also benefit from the p2p feature propagating queries on the network.

Item and test types
-------------------

1.  HAWAI: there should be a way to design behaviors on items, like for instance stating that if the user clicks on the button I put in the item, that my picture of a hot air balloon should go up. This enables the creation of little simulations in order to assess, for example, complex problem solving.
2.  Custom test type : There should be a possibility to import a custom open web test, similarly to what is possible at the level of items.

### Generis : Picture label

We could associate to every resources a picture (whatever which extension) and browse resources as a gallery. (Feature \#515)

### Collect usage data on resources.

Collect informations/statistics about the use made of resources.

### Recursive forms embedding

When editing a resource, for some of the properties, fields you may point to a resource (the property is a relation). It should be possible to recursively describe this connex resource within the main form and using an embeded form.\
h2. TAO 2.X Ease of Use

TAO is a full-fledged platform highly customisable. This flexibility brings complexity. The plan is not to reduce the available functionality but optimize features presented to user by either :

### 1. Persona’s

\> Targeting a specific type of users. (Ex.: teachers) and provide them with additional speciifc extensions adapting vocabulary, personalizing user interfaces and hiding less relevant capabilities or settings.\
h3. 2. Follow the learning curve.\
\> Implementing different usage settings in capabilities : Simple, Advanced, Expert modes.

In all cases, users may access all the functionality if wanted.

Detailed plans will follow based on the feedback we collect from the usability testing and our ergonomic experts.

Graphical User Interface improvement and more user-friendly functional design\
Intuitively and efficiently navigate through self-explanatory functionalities and interfaces

Redesigned and easy-to-use advanced test authoring tool\
Create advanced tests and reduce test-taking time by easily designing conditional item flows and dynamic tests reflecting individual performances.
