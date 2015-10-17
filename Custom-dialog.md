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
