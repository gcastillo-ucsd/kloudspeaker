Kloudspeaker uses [Durandal](http://durandaljs.com/) for creating views and binding them with model objects.

This allows creating UI that have both, view and model, defined with modules. Views can be preloaded templates or HTML files, and models JavaScript module classes with data. With [Knockout](http://knockoutjs.com/) binding tools, view and model can be tied together without coding the UI logic.

# View and model binding

View and model binding is done with observables, fields that can be observed for changes. If field is bound to input field, it is automatically updated if the value is changed in the model. And the same way, if user changes the value in input, the model is updated automatically.

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

In this example, model creates observable field "name", which is bound to input field. Second element, span, is also bound to same field, and is updated automatically if user changes the value.

Clicking the button will trigger the function "onClick", which will show alert box with the name user gives.

For details on creating views and modules, see http://durandaljs.com/documentation/Creating-A-View.html

For binding tools, see http://knockoutjs.com/documentation/introduction.html

# Using views and models

## Full views

Using module "kloudspeaker/ui/views" it is possible to register full application views.

    views.registerView("myview", function(rqParts, urlParams) { ... });

This will register view handler for view id "myview". When browser opens URL "http://yoursite/kloudspeaker?v=myview", this function is called.

Param rqParts is array with view id parts, for example if view opened is "?v=myview/subview", the array is ["myview", "subview"].

Param urlParams contains all parameters in the request.

The function can return
* false if no view should be opened
* object with model (and optionally view) for UI composition

For example:

    views.registerView("myview", function(rqParts, urlParams) {
        return {
            model: 'my-package/myview'
        };
    });

This will load module 'my-package/myview' as the view and model: for a view, it loads "my-package/myview.html" as a view, and "my-package/myview.js" as model.

It is possible to define separate view module:

    views.registerView("myview", function(rqParts, urlParams) {
        return {
            model: 'my-package/myview',
            view: 'my-package/templates/myview'
        };
    });

## Dialogs

Creating a dialog with view & model, use Kloudspeaker module 'kloudspeaker/ui/dialogs':

    dialogs.custom({
        title: 'My Dialog Title',
        model: 'my-package/module',
        buttons: [{
            id: "no",
            "title": kloudspeaker.ui.texts.get('dialogClose')
        }]
    });

This will load module 'my-package/module' as the view and model: for a view, it loads "my-package/module.html" as a view, and "my-package/module.js" as model.

It is possible to define separate view 

    dialogs.custom({
        title: 'My Dialog Title',
        view: 'my-package/templates/module',
        model: 'my-package/module',
        buttons: [{
            id: "no",
            "title": kloudspeaker.ui.texts.get('dialogClose')
        }]
    });

To pass data into model module, use array syntax:

        model: ['my-package/module', someObj]

And in model module, define function "activate" which is called when model is activated, with the someObj as parameter.

    define([deps], function(...) {
        return {
            activate: function(someObj) {
                // initialize model
            }
        }
    });

## Config views

TODO

## Manual composition

If it is needed to use UI composition manually, it is possible to do with module kloudspeaker/ui:

    ui.viewmodel(view, model, $target)

where
* view defines the view to be bound (can be module id, template id or actual DOM object)
* model defines the model to be bound (can be module id or actual model object)
* $target is the DOM object where view is inserted into