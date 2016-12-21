<!--
parent:
    title: Workflow_Engine
author:
    - 'Jérôme Bogaerts'
created_at: '2011-03-10 11:42:08'
updated_at: '2013-03-13 13:03:47'
tags:
    - 'Workflow Engine'
-->

{{\>toc}}

Workflow API
============

The Workflow API is a Javascript library which enables you to access and drive the workflow from an item, a service.

1. Download
-----------

You can either:

-   download the Workflow API standalone package here : attachment:wfapi.zip
-   use the version included in the TAO distribution at /wfEngine/views/js/wfApi

2. API
------

The Workflow API provides the following services:

-   control the flow of the process (backward, forward, pause)
-   define what to do when the activity is finished
-   define that the activity is finished
-   save and retrieve contextual data used to recover the state of your activity when you go back on it or after a crash.

You can find all the documentation of the methods and useful examples in the package.

3. Interface
------------

The interface below is an overview of the available methods:

### 3.1. Workflow controls

    /**
     * Trigger the forward control:
     * go to the next activity
     */
    function forward();

    /**
     * Trigger the backward control:
     * load to the previous activity
     */
    function backward();

    /**
     * Trigger the pause control:
     * suspend the current activity and go back to the process control panel
     */
    function pause();

### 3.2. Finish event handlers

    /**
     * Define the item's state as finished.
     * This state can have some consequences.
     */
    function finish();

    /**
     * Add a callback that will be executed on finish state.
     */
    function onFinish(callback);

    /**
     * Add a callback that will be executed on finish but before the other callbacks  
     */
    function beforeFinish(callback);

    /**
     * Add a callback that will be executed on finish but after the other callbacks  
     */
    function afterFinish(callback);

### 3.3. Recovery

    /**
     * Initialize the interfaces communication for the context recovery.
     * The source service defines where and how we retrieve contexts.
     * The destination service defines where and how we send/save the contexts.
     */
    function initRecoveryContext(source, destination);

    /**
     * Retrieve the context identified by the key 
     */
    function getRecoveryContext(key);

    /**
     * Set, send and save a context that could be recovered 
     */
    function setRecoveryContext(key, data);

    /**
     * Remove a context (once you don't need you to recover it anymore) 
     */
    function deleteRecoveryContext(key);