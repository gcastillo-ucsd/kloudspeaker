Using Kloudspeaker JavaScript API, it is possible to create UI with two methods: templates and UI binding.

## Templates

TODO

## UI binding

Kloudspeaker supports UI binding using KnockoutJS library. It allows creating UI that is bound to JavaScript model, automatically updating when either UI or model changes.

Bound UI API is under development, and is subject to change.

For now, dialogs can use bound UI with following API:

    var model = new MyDialogModel(item);
    kloudspeaker.ui.dialogs.custom({
        title: 'My dialog name',
        template: ["my-dialog-tmpl", {
            title: "Some parameter for template"
        }],
        model: model,
        buttons: [{
            id: "no",
            "title": kloudspeaker.ui.texts.get('dialogClose')
        }],
        "on-button": function(btn, d) {
            d.close();
        }
    });

And model definition any JS object:

    var MyDialogModel = function(item) {
        var that = this;
        this.name = ko.observable();

        this.onAttach = function() {
            // called when UI is bound
            that.name(item.name);
        };

        this.onSave = function() {
            // handle saving
            return true;
        };
    };

And UI template

    <script id="my-dialog-tmpl" type="text/x-jquery-tmpl">
        <div class="test">
            My dialog: ${title}<br/>
            
            Name: <span data-bind="text: name"></span><br/>

            <input data-bind="value: name" /><br/>
        </div>
    </script>

This example shows how field "name" is bound to the model, and editing the value automatically updates the field in UI.