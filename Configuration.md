# Introduction

Kloudspeaker app has two configurations
* Client configuration
* Backend configuration

# 1. Client configuration

Client configuration is defined in the application web page (`index.html`), and installation package has an example page.

## 1.1. Syntax

Application is configured in the js app initialization, and the syntax of the initialization call is following:

    <script type="text/javascript">
        $(document).ready(function() {
            require(['kloudspeaker/app'], function(app) {
                app.init({
                    ... // CONFIGURATION OPTIONS
                });
            });
    </script>

For all possible configuration options, see [[Client Configuration Options | Client-configuration-options]].

## 1.2. Plugin configuration

Client plugins are configured in the init call plugins array, for example:

    <script type="text/javascript">
        $(document).ready(function() {
                kloudspeaker.App.init({
                                ...
                        },
                        [
                                new kloudspeaker.plugin.PluginA(),
                                new kloudspeaker.plugin.PluginB()
                        ]
                );
        });
    </script>

Possible plugin options can be passed in the plugin constructor, for example:

    new kloudspeaker.plugin.PluginA({
        "plugin_option_1" : "value",
        "plugin_option_2" : "value2"
    })

See [[available plugins | Plugins]] and plugin specific configuration instructions.
# 2. Backend configuration

Backend configuration file is "`configuration.php`" located under folder "`backend`". Example configuration files can be found from "`backend/examples`".

## 2.1. Syntax

Syntax of the "`configuration.php`" is following:

	$CONFIGURATION = array(
		"option_key" => "value",
		"option_key_2" => "value2"
	);

At minimum, define option "`db`" for database configuration, see chapter "2.2. Database" below.

For all possible configuration options, see [[Backend Configuration Options | Backend-configuration-options]].

## 2.2. Database

Kloudspeaker supports MySQL and SQLite databases, either directly or via PDO interface.

### 2.2.1. MySQL

Before installing Kloudspeaker, create MySQL user and database for Kloudspeaker, and grant the new user CREATE/INSERT/UPDATE/DELETE rights for the created database.

Create configuration file with MySQL database information, for example:

	$CONFIGURATION = array(
		"db" => array(
			"type" => "mysql",
			"user" => "kloudspeaker",
			"password" => "kloudspeaker",
	
			"host" => "localhost", // optional
			"database" => "kloudspeaker", // optional
			"table_prefix" => "kloudspeaker_", // optional
			"charset" => "utf8" // optional
	
			"engine" => "innodb" // optional, used only in installation
		),
	);

Values "`host`", "`database`", "`table_prefix`" and "`engine`" are optional. If these are not defined, it is assumed that MySQL server is running on localhost, database is called "`kloudspeaker`" and tables are accessed without name prefix.

With localhost database, you can also provide socket for the connection:

        "socket" => "/tmp/mysql5.sock"

Default MySQL engine used is InnoDB. With option "`engine`" you can change this (**NOTE** used only on installation).

        "engine" => "myisam";

Using MySQL via PDO can be configured like this:

	$CONFIGURATION = array(
		"db" => array(
			"type" => "pdo",
			"str" => "mysql:host=localhost;dbname=kloudspeaker",
			"user" => "kloudspeaker",
			"password" => "kloudspeaker",
	
			"table_prefix" => "kloudspeaker_", // optional
			"charset" => "utf8" // optional
		),
	);

### 2.2.2. SQLite

Create configuration file with SQLite database information, for example:

	$CONFIGURATION = array(
		"db" => array(
			"type" => "sqlite",
			"file" => "db.file"
		),
	);

Value "`file`" defines the location of the SQLite database file. **NOTE** Using absolute path is recommended.

For SQLite version 3, use type value "`sqlite3`".

Using SQLite via PDO can be configured like this:

	$CONFIGURATION = array(
		"db" => array(
			"type" => "pdo",
			"str" => "sqlite:kloudspeaker.db",
			"user" => "kloudspeaker",
			"password" => "kloudspeaker"
		),
	);

## 2.3. Plugin configuration

Backend plugins are defined in option "plugins" with following syntax:

	$CONFIGURATION = array(
		...
	
		"plugins" => array(
			"PluginA" => array(),
			"PluginB" => array()
		)
	);

Each plugin can have configuration options that are defined in the PHP array, for example:

	$CONFIGURATION = array(
		...
	
		"plugins" => array(
			"PluginA" => array(
				"plugin_option_1" => "value",
				"plugin_option_2" => "value2",
			),
			"PluginB" => array()
		)
	);

See [[available plugins | Plugins]] and plugin specific configuration instructions.