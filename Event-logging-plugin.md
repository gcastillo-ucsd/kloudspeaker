Event logging plugin is built-in plugin that provides logging all user actions, and viewing them via admin tool.

## Configuration

Configure plugin with following configuration:

	$CONFIGURATION = array(
		...,
		"plugins" =>
			"EventLogging" => array()
		)
	);

Plugin has following settings:
  * logged_events

Logged events is optional, and limits the event types logged. If this setting is defined, all events with matching id will be logged (wildcard match is done automatically). To log all events, leave this setting out.

For example, to log only filesystem and session events, use following configuration:

	"EventLogging" => array(
		"logged_events" => array("filesystem/", "session/")
	)