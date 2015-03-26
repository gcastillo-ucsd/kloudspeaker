Kloudspeaker can send emails on many occasions, for example on user registration or Notificator plugin.

To enable mail sending, configure it with following settings:

	$CONFIGURATION = array(
		"enable_mail_notification" => TRUE,
		"mail_notification_from" => "admin@yourhost.com",
		...
	);

Setting "mail_notification_from" defines the sender address (and optionally also name) used in mails (for example "`admin@yourhost.com`", "`Administrator admin@yourhost.com`"). If no value is given (default), mail is sent with system default.

## PHPMailerSender

Default mail sender uses PHP internal mail functionality.

It is possible to use third-party mail sender library [PHPMailer](https://github.com/PHPMailer/PHPMailer) by changing the sender class:

	$CONFIGURATION = array(
		"enable_mail_notification" => TRUE,
		"mail_notification_from" => "admin@yourhost.com",
		"mail_sender_class" => "mail/PHPMailerSender.class.php",
		"mail_smtp" => array(
			"host" => MAIL_SERVER_HOST,
			"username" => USERNAME,
			"password" => PASSWORD,
			"secure" => TRUE
		)
		...
	);

To use SMTP server, add following configuration:

	$CONFIGURATION = array(
		"mail_smtp" => array(
			"host" => MAIL_SERVER_HOST,
			"username" => USERNAME,
			"password" => PASSWORD,
			"secure" => "tls"/"ssl"
		)
		...
	);

The option "secure" defines whether mail sending is done via TLS (value "tls") or SSL (value "ssl"), leave out to use non-secured connection.