It is possible to create custom plugins for Kloudspeaker in client and backend.

Client plugins can add content and functionality in the UI, and backend plugins can create new services and extend existing functionality.

Both can be registered separately, but it is also possible to create a backend plugin package that contains also client plugin, which allows making individual packages containing all functionality from UI to backend.

## Client plugins

Client plugins are registered in index.html

    <script type="text/javascript">
        $(document).ready(function() {
            kloudspeaker.App.init({
                ...
            },
            plugins: {
                new CustomPlugin()
            }
        });
    </script>

The plugin itself is expected to be a javascript object with at least variable `id` defining unique identifier for the plugin.

    var CustomPlugin = function() {
        var that = this;

        return {
            id: "custom-plugin"
        }
    };

For other options in JavaScript plugins, see JS plugin API.