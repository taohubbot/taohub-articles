<!--
parent: 'Documentation for core components'
created_at: '2015-03-11 08:50:10'
updated_at: '2015-03-11 08:50:10'
authors:
    - 'Antoine Robin'
tags:
    - 'Documentation for core components'
-->

How to develop a Javascript Component
=====================================

You want to develop a Javascript component to use it from several place of you application. Before starting the development there are some things you have to know and some questions you have to think about.<br/>

First of all you will have to chose between a javascript plugin or a JQuery plugin. Javascript plugin are often a template that you want to have on many page and configure it a little. Jquery plugin are more about modifying or adding some functionality to an existing DOM element.<br/>

Now you have to thing about the purpose of your plugin, feature you want it to have. So you will be able to find an API, a list of method it will expose, and start the development of your pugin.

JQuery Plugin
-------------

JQuery plugin contains one core variable, this variable will contains all the properties and methods of the api. We can have extra variables used in the core variable. The core variable will contains an init method, the one that will be called on the initialization of the module and other methods that you found when you thing about the API.

    var myPlugin = {
        init : function(options){

            return this;
        },
        method1 : function(){

        },
        method2 : function(){

        },

    }

Once you implemented your plugin you have to expose some of its method to get it working to do that you will need Pluginifier to register the methods to expose.

    Pluginifier.register(ns, myPlugin, {
        expose : ['method1', 'method2']
    });

Pluginifier is a tool that will turn your JQuery script into a plugin. You will be able to use it as a JQuery plugin (ie `$("#selector").myPlugin();`). This will also expose methods that you want them to be public. This methods have to be in the option `expose` as an array. After that you can use these methods like `$("#selector").myPlugin('method1');`.

Javascript Plugin
-----------------

We will see how to make a Javascript plugin throught an exemple. Let’s say that you want to display a box with a message on your pages and you have a common template even if the message is different. Then when you click on a button it will call an url and return something.<br/>

To do this you will need three variables, the Api that contains all the methods that you will need for your plugin, the factory, that will instanciate a new object and a state that will contains the state of your object and modify this state.

    var myApi = {
        myProperty : null,
        myMethod : function myMethod(arg1,arg2){
        }
    }

The API will contains all the core properties and methods of your plugin. In the exemple we will have for exemple a method to create the template in the state we want, with the correct message and the correct options. Another will display this message by putting the content into the right container and bind the click on the button to call the method that we configure on initialization. And surely a last one to close the message and clear the instance.

    var myState= {
        state : null,
        getState : function getState(){
            return state;
        },
        setState : function setState(myState){
            this.state = myState;
        }
    }

Thanks to this object we will be able to set and get the state of the object, for exemple is it opened, displayed or closed ? these information will be helpful to do different actions for different states.

    var myFactory = function myFactory(container){

            var plugin = _.extends({
                id          : 'uniqueId',
                _container  : container
            },myState);

            //delegate the api calls to the new instance
            return delegate(plugin, lockApi);
    }

Here we just instantiate a new object, we also can verify if the container exists and do actions before returning the created object.

    function delegate (receiver, provider) {
        _(provider).functions().forEach(function delegateMethod(methodName) {
            receiver[methodName] = function applyDelegated() {
                return provider[methodName].apply(receiver, arguments);
            };
        });
        return receiver;
    }

This method allows us to separate the API from the factory. Each object will be able to call the API function without having them in its definition.

The plugin will be based on a template that you have to put in a folder with the same name as you plugin (by convention) and require it by adding `'tpl!path/to/template'` to the require array. The in your plugin you can get the content of the template by calling

    tpl({
        arg1 : this.myProperty,
        msg : msg
    });

In your template you can display the different parameters with the `{{arg1}}` structure.

Unit Test
---------

Unit tests should be mostly write before the plugin code but you can execute them only when the plugin is finalize.<br/>

First create a folder named as your plugin that contains a test.html and a test.js





                Ui Test - Lock







                    //don't start the test now
                    QUnit.config.autostart = false;

                    //load the config
                    require(['/tao/ClientConfig/config'], function(){

                        //load the test
                        require(['path/to/your/test'], function(){

                            //Tests loaded, run tests
                            QUnit.start();
                        });
                    });










the `<base/>` should refere to the tao/views folder in order to load correct js and css. with this code you will load all librairies that are needed to launch your tests. You can also add blanket `js/lib/blanket/blanket.min.js`.<br/>

You can put all you want in the <br/>
#qunit-fixture div, this will be cleaned after each test so you will not have side effect.

    define(['jquery', 'your/plugin'], function($, plugin){
        'use strict';
        QUnit.module('plugin');

        QUnit.test('module', function(assert){
            QUnit.expect(1);

            assert.ok(typeof plugin === 'function', 'The module expose a function');
        });

    });

This script javascript is used to test the plugin. You can have more information on how to test your plugin here : http://api.qunitjs.com/.


