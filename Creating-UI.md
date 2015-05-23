Kloudspeaker uses [Durandal](http://durandaljs.com/) for creating views and binding them with model objects.

Views can be preloaded templates or HTML files, and models JavaScript objects. With [Knockout](http://knockoutjs.com/) binding tools, view and model can be tied together without coding the UI logic.

It is suggested to create both, view and model, as independent modules. See https://github.com/sjarvela/kloudspeaker/wiki/Client-modules

# View and model binding

View and model binding is done with observables, fields that can be observed for changes. If model field is bound to input field, it is automatically updated if the value is changed in the model. And the same way, if user changes the value in the input field, the model is updated automatically.

Example model:

        var model = {
            name: ko.observable('')
        };
        return {
            activate: function(params) {
                // retrieve data etc
                model.name(params.name);
            },
            model: model,
            onClick: function() {
                alert(model.name());
            }
        };

Example view:

    <div>
        <input type="text" data-bind="value: model.name" autofocus></input>
        <span data-bind="text: model.name"></span>
        <button data-bind="click: onClick">Click</button>
    </div>

In this example, model creates observable field "`name`", which is bound to input field. Second element, span, is also bound to same field, and is updated automatically if user changes the value.

Clicking the button will trigger the function "`onClick`", which will show alert box with the name user gives.

For details on creating views and modules, see http://durandaljs.com/documentation/Creating-A-View.html

For binding tools, see http://knockoutjs.com/documentation/introduction.html

# Using views and models

## Full views

Using module "`kloudspeaker/ui/views`" it is possible to register full application views.

    views.registerView("myview", function(rqParts, urlParams) { ... });

This will register view handler for view id "`myview`". When browser opens URL "`http://yoursite/kloudspeaker?v=myview`", this function is called.

Param rqParts is array with view id parts, for example if view opened is "`?v=myview/subview`", the array is `["myview", "subview"]`.

Param `urlParams` contains all parameters in the request.

The function can return
* `false` if no view should be opened
* object with `model` (and optionally `view`) for UI composition

For example:

    views.registerView("myview", function(rqParts, urlParams) {
        return {
            model: 'my-package/myview'
        };
    });

For options `model` and `view`, see Composition.

Example for full view can be found at [Registration plugin](https://github.com/sjarvela/kloudspeaker/blob/master/backend/plugin/Registration/client/main.js)

## Dialogs

Creating a dialog with view & model, use Kloudspeaker module `kloudspeaker/ui/dialogs`:

    dialogs.custom({
        title: 'My Dialog Title',
        model: 'my-package/module',
        buttons: [{
            id: "no",
            "title": kloudspeaker.ui.texts.get('dialogClose')
        }]
    });

Optionally, view can be defined with `view`.

For options `model` and `view`, see Composition.

Example for dialog is user dialog: [model](https://github.com/sjarvela/kloudspeaker/blob/master/js/kloudspeaker/config/user/addedit.js) and [view](https://github.com/sjarvela/kloudspeaker/blob/master/templates/kloudspeaker/config/user/addedit.html)

## Config views

Config views can be registered with module `kloudspeaker/ui/views`:

        views.registerConfigView({
            viewId: 'myconfig',
            title: 'Config view title',
            model: 'my-package/plugin/config'
        });

This registers a config view that will be accessible with url "`?v=admin/myconfig`", and will be in the navigation menu with title "Config view title". If localized text is shown, it can be given with "`i18n:textKey`".

Optionally, view can be defined with `view`.

For options `model` and `view`, see Composition.

## Manual composition

If it is needed to use UI composition manually, it is possible to do with module `kloudspeaker/ui`:

    ui.viewmodel(view, model, $target)

Parameter $target is the DOM object where composed view is inserted into. For parameters "`view`" and "`model`", see Composition.

# Composition

With any composition use case (full view, dialog, config view etc), following options are available:

Model definition can be
* module id to be loaded via require.js
* array, where first item is module id, and all rest will be passed to module activation params
* model object instance

View definition can be
* module id to be loaded via require.js
* template id with syntax "#template-id" (template must be preloaded)
* DOM object

If model is module id, and view is not defined, then same module id is used. In this case model will be loaded with "`.js`" extension and view with "`.html`" extension (or if template is optimized, with require.js text "`text!`" prefix).

To pass data into model module, use array syntax for model:

        ['my-package/plugin/config', someObj]

When view is activated, model function "`activate`" is called. If there are data passed as parameter, they are passed as function params.

    define([deps], function(...) {
        return {
            activate: function(someObj) {
                // initialize model
            }
        }
    });