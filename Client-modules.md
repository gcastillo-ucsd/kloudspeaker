Kloudspeaker client is built with modular (using AMD&require.js) design, where different services and interfaces are published as independent modules.

For different Kloudspeaker modules available, see https://github.com/sjarvela/kloudspeaker/wiki/Client-API

Own modules can be loaded with module definition in index.html

    $(document).ready(function() {
        kloudspeaker.App.init({
            "modules": {
                load: ['my-package/plugin'],
                paths: {
                    'my-package': '/path/my-package/'
                }
            },
            ...
        });
    });

Any loaded modules can be added to the array "module/load", and they will be resolved via require.js rules.

To define package location, field "module/paths" can be used. In this example, it defines that package "my-package" will be found at "/path/my-package/", and so loading any module under "my-package" is resolved into this folder.

To define Kloudspeaker plugins using modules, see https://github.com/sjarvela/kloudspeaker/wiki/Plugin-development