Config views can be registered with module `kloudspeaker/ui/views`:

        views.registerConfigView({
            viewId: 'myconfig',
            title: 'Config view title',
            model: 'my-package/plugin/config'
        });

This registers a config view that will be accessible with url "`?v=admin/myconfig`", and will be in the navigation menu with title "Config view title". If localized text is shown, it can be given with "`i18n:textKey`".

Optionally, view can be defined with `view`.

For options `model` and `view`, see Composition.