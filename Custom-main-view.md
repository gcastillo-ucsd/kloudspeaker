It is possible to create custom main views that are listed in the toolbar next to "Files" and "Configuration".

1) Registering custom module

In kloudspeaker client init

    "modules": {
        load: ['kloudspeaker/ui/dropbox', 'my-package'],
        paths: { 
            'my-package': '/path/to/my-package' }
        }
    }
    
2) Create folder "my-package" into path defined above

3) Create main module

Create file "main.js" into folder "my-package"

    define(['kloudspeaker/ui/views'], function(views) { 
        views.registerMainView({
            id: 'help',
            title: 'i18n:helpViewTitle', 
            icon: 'question',
            view: 'my-package/main-help-page.html'
        });
    });

4) Create "main-help-page.html" into folder "my-package"

This will show new view called "help" in toolbar. Title will be loaded with localized key "helpViewTitle" and has Font Awesome icon with id "question".

## Navigation

With custom main view, it is possible to define navigation bar items

        views.registerMainView({
            nav: [
                // items
            ]
        });

Each nav item is object with at least type and title.
* type "heading" you can display subtitle
* type "link" will create static link, url should be given with property "url"
* type "view" will create pointer to subview

Example

        views.registerMainView({
            id: 'help',
            title: 'i18n:helpViewTitle', 
            icon: 'question',
            view: 'my-package/main-help-page.html',
            nav: [{
                type: 'heading',
                title: "Title"
            }, {
                type: 'view',
                id: 'subview1'
            }, {
                type: 'view',
                id: 'subview2'
            }, {
                type: 'heading',
                title: 'Title2'
            }, {
                type: 'link',
                title: 'Link',
                url: 'http://some.link'
            }]
        });

## Subviews

With custom main views, it is possible to publish subviews.

    views.registerMainView({
        subviews: [
            // views
        ]
    });

Each view definition has id (to be referred, for example, in nav definition) and title. Depending on view type, it can have
* only 'view' if static html page is loaded
* model with optional view to load custom view module

For example

        subviews: [{
            id: 'subview1',
            title: 'i18n:subView1Title',
            view: 'my-package/subview1.html'
        }, {
            id: 'subview2',
            title: 'i18n:subView2Title',
            model: 'my-package/subview2'
        }]

This defines two views: "view1" with static html page "subview1.html" and "view2" that loads module "my-package/subview2" with a view with same name. See [composition](https://github.com/sjarvela/kloudspeaker/wiki/Creating-UI#composition)