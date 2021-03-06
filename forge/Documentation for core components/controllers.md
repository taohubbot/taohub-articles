<!--
parent: 'Documentation for core components'
created_at: '2011-03-04 17:36:10'
updated_at: '2014-10-03 10:40:20'
authors:
    - 'Joel Bout'
contributors:
    - 'Bertrand Chevrier'
tags:
    - 'Documentation for core components'
-->

Controllers
===========



![](http://forge.taotesting.com/attachments/download/760/attention.png) The information on these page relates to Tao 2.5 or earlier and might not reflect the current version.

As explained previously, in the ClearFw, a MVC **controller** is called a **module**. We will be referring to *module classes* in this context.

URL Mapping
-----------

The module classes (the controllers) provide a set of actions to be executed regarding the user workflow (the http request). The purpose of these actions is to manage view rendering that are populated by the data loaded from the business model. You can get more details regarding this behavior by having a look at the MVC documentation (see [Wikipedia](http://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller)).<br/>

To summarize this approach: a user requests an action. This action is executed by the controller layer and renders a view with the data extracted by the model.

TAO extensions take advantage of the *URL rewriting* for the action mapping. Each URL of the application is mapped to a particular action.<br/>

When a user requests a URL of the TAO application, a mechanism called *dispatching* looks for the right action to execute it. You need to understand those principles to call actions into TAO.

The URLs into TAO are not formatted to refer to resources (i.e., a PHP file). They contain information that will be used to find the actions to be executed.<br/>

A URL contains the following information:

-   the target extension
-   the name of the module (the controller)
-   the method to calls into this class (the action)
-   some key/value parameters (as usual)

For example, have a look at the following URL:

> `http://www.tao.lu/tao/Users/add?name=john`

If you split the URL, each part is used as a piece of information for the mapping:<br/>

|*.Token|*.Information|<br/>

|`www.tao.lu`| the TAO domain name|<br/>

|tao| the extension name (the meta-extension TAO)|<br/>

|Users| the module name|<br/>

|add| the action name|<br/>

|name=john| the parameters|

By calling this URL the method `add` of the class *tao_action_Users* in the `tao` meta-extension will be executed:

      tao_action_Users::add($_GET['name']);

The mapping is made by a *Resolver* using requests analysis. Of course, there is no resource */tao/Users/add* (file or CGI script) in the web server.<br/>

For each request matching a given format, the main entry file is executed (`extensionName/index.php`) and so, the dispatching loop is launched.<br/>

This mechanism is available thanks to the *mod_rewrite* of the Apache web server.

Actions structure
-----------------

The following schema shows you the structure of the *actions*. You must respect some conventional rules to create actions.

-   *Module* class from ClearFw is the parent class of all the modules.
-   The TAO meta-extension provides 2 classes to create actions into TAO:
    -   The *tao_actions_CommonModule* class which provides a weak integration, like the user authentication verification. For example, the module class *tao_actions_Main* is the main entry point of the TAO back-office and extends *tao_actions_CommonModule*
    -   The *tao_actions_TaoModule* class provides a strong integration with the TAO interface. For instance, the items, tests or groups modules classes extend the TaoModule.

![](http://forge.taotesting.com/attachments/385/actions.png)

Workflow
--------

The *actions* folder of the extensions contains a *structure.xml* file. This file describes how the actions are organized, structured and it provides mapping with the UI components (menu, tree, action box, etc.).

For example, a tree widget is populated with JSON data. The *structure.xml* file gives the URL to get the data into a particular context.

The format of this XML file is described in the following DTD (comments are explicit about the tags and attributes usage):

-   [structure.dtd](https://github.com/oat-sa/tao-core/blob/master/doc/structures.dtd)

A sample structure.xml file:

-   [structure.xml](https://github.com/oat-sa/tao-core/blob/master/actions/structures.xml)

The TAO extension is the main entry point for any request. The URL */tao/Main/index* is called with the browser and contains the extension and section parameters.<br/>

The main action is called, loads the appropriate *structure.xml* file and renders a main template (it’s a global container). The components, widgets, forms, etc of the current extension/section are initialized regarding the context parameters, the data from the *structure.xml* file and the session. It provides us with a general frame of navigation where extensions only have the role of specialization.

The initialization workflow is detailed in the following schema:

![](http://forge.taotesting.com/attachments/386/tao-actions-nav.png)

**structure.xml definition:**

![](http://forge.taotesting.com/attachments/download/158/structure_xml_hierarchie.png)

-   TAG *extension*: the current extension
    -   Attribute *name*: the extension name, displayed in the menus (used as translation key)
    -   Attribute *url*: the page/action to be loaded by default when the user selects the extension
    -   Attribute *level*: to order the extensions in the menus
-   TAG *sections*: contains some sections
-   TAG *section*: represents a logical section of the extension (displayed into the UI tabs), the choice of the section cutting is let to the analyst
    -   Attribute *id*: a unique identifier of the section
    -   Attribute *name*: the displayed section name (used as translation key)
    -   Attribute *url*: the page/action to be loaded by default when the user selects the section

The *structure.xml* file describes the navigation structure of an extension as seen previously. It also contains the description of the interface widgets. Because the UI of TAO uses extensively the client sides component, the structure file provides information regarding: the widgets navigation, the actions, the interactions with others actions, the data population, etc.

Now, the *section* tag can contain 2 different widgets:

-   Trees
-   Contextual actions box

The following schema illustrates the way the action widget works:

![](http://forge.taotesting.com/attachments/387/actions_widget.png)

|


