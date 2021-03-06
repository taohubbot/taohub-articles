<!--
parent: 'Documentation for core components'
created_at: '2011-03-04 17:31:25'
updated_at: '2013-03-21 15:18:15'
authors:
    - 'Joel Bout'
contributors:
    - 'Bertrand Chevrier'
tags:
    - 'Documentation for core components'
-->

Extensions
==========



TAO extensions enable the use of other extensions handling concepts and relations that define the domain. They cover all phases of the assessment process, from authoring, planning and other administration back-office operations, to delivery, result collection and analysis. The incorporation of these concepts in the platform is performed thanks to its modular architecture.<br/>

Each knowledge domain corresponds to an independent data domain that can be managed by different actors possibly distributed in various locations (subjects, groups, tests, items and results). For instance, and in order to ensure privacy, the management of subjects and their characteristics is managed apart from groups.

![](http://forge.taotesting.com/attachments/542/extension_model.png)

1. TAO Architecture
-------------------

This section covers the architecture of the TAO platform. It’s built upon the concept of extensions. Each extension is composed of a separated file-system. They contain the same folder structure in order to be exploited by the TAO Framework.<br/>

An extension may be used as a standalone program - with the exception of an extension depending on another extension. This concept of extension dependencies enabled us to create TAO extensions using abstraction layers and core components.

The following schema illustrates this:

![](http://forge.taotesting.com/attachments/download/2239/extensions.png)

As you can see above, the Generis and TAO extensions are dependent on all other extensions. The Generis extension contains the framework [ClearFw](http://code.google.com/p/clearfw/) and the APIs. The TAO extension provides the application layers.

2. TAO meta-extension
---------------------

TAO extension is a *meta-extension*. In other words, this extension cannot be used as a standalone, but it provides high-level components that will be used by their dependent extensions (i.e., items, subjects or groups).

The TAO meta-extension is **required** to run any other extension. It provides the architecture for the application layers that the dependent extensions will use or change. For example, the TAO extension provides a mechanism to check if a user is authenticated. All extensions that need a logged in user will use that mechanism directly into the TAO extension.<br/>

In order to use a layer from the meta-extension, the dependent extension’s classes *extend* the TAO extension classes. In our example, the authentication is done by default if the extension’s actions extends the TAO’s *tao_actions_CommonModule* class. To change the behavior provided by the meta-extension, you can override the concerned methods.

-   The TAO meta-extension provides the architecture with different layers:
    -   **Model** : the main business model is provided by a service oriented mechanism
    -   **View** : the user interface structure and components: widgets, style sheets, templates, etc.
    -   **Controller** : the user workflow and navigation through simple actions



-   and contains transverse functionalities:
    -   the bootstrap to start the application loop
    -   the authentication and user management
    -   the common helpers
    -   the dynamical form engine

|

3. Extension’s Structure
------------------------

Each extension is built upon the [ClearFw](http://code.google.com/p/clearfw/) a really simple php5 MVC framework. This framework provides basic functionalities to develop web applications according to some very simple and good practices…<br/>

The current release of TAO is built on the evolution of the framework that can be found [here](http://clearfw.googlecode.com/svn/tags/taoTransfer) .

Each extension uses and extends this model. From the point of view of the file-system, an extension is contained into a folder. The folder’s name is the extension’s name. Even though there are dependencies among the extensions, they are all at the same level of the file-system, into your *TAO distribution* directory.

The screenshot below represents a TAO distribution into the *transferAll* folder, that contains the usual extensions:

![](http://forge.taotesting.com/attachments/394/extension_filesystem.png)

Inside an extension we have the following folders structure:

-   **actions**<br/>

    It contains the controller layer.
    In the ClearFw, a **controller** is called a **module**. We are using this convention.
    The *actions* folder contains all the module classes (the controllers) of the extension and can also contain a *structure.xml* file that describes the User Interface structure.



-   **helpers**<br/>

    It contains all utility class: the shared components (the dynamic form component), the transverse functionalities (security) and some common utilities (Uri or String helper)



-   **includes**<br/>

    It contains the configuration files, constant files and may also contain the Bootstrap.



-   **install**<br/>

    It contains an extension specific data and scripts to install the extension. The SQL Database, the RDF Model and PHP scripts to be executed during the installation



-   **locales**<br/>

    The framework handles internationalisation. Locale variables are stored in file *messages.po* in a directory corresponding to the language. For example, locales/EN/messages.po contains the translation file for English. We use the *gettext* format.



-   **models**<br/>

    It contains the data models of the extension and the business classes. The manipulation of the model is made through a service layer. The **services** provide methods to manage the data from any data source. We usually create services to manage RDF models through the *Generis API*, row data from the database, files or web-services.



-   **scripts**<br/>

    It contains command lines or utility scripts.



-   **test**<br/>

    It contains Unit Tests.



-   **views**<br/>

    It contains the view layer: the HTML templates, the common web resources like images, style-sheets and client-side scripts



-   /<br/>

    The root of the extension contains the front bootstrap *index.php*, the ExtensionManifestDescription|extension description file *manifest.php* and the web server configuration file *.htaccess* (describing the URL rewriting, the redirections and the authentication rules).

|


