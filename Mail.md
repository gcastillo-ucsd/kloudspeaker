Kloudspeaker can send emails on many occasions, for example on user registration or Notificator plugin.

To enable mail sending, configure it with following settings:

	$CONFIGURATION = array(
		"enable_mail_notification" => TRUE,
		"mail_notification_from" => "admin@yourhost.com",
		...
	);

Setting "mail_notification_from" defines the sender address (and optionally also name) used in mails.

For example, values can be given with address only "`admin@yourhost.com`", or with address and name "`Administrator admin@yourhost.com`").

If no value is given (default), mail is sent with system default.

## PHPMailerSender

Default mail sender uses [PHP internal mail](http://php.net/manual/en/book.mail.php) functionality, which sends mail as configured in the PHP server configuration.

It is possible to use third-party mail sender library [PHPMailer](https://github.com/PHPMailer/PHPMailer) by changing the sender class:

	$CONFIGURATION = array(
		"enable_mail_notification" => TRUE,
		"mail_notification_from" => "admin@yourhost.com",
		"mail_sender_class" => "mail/PHPMailerSender.class.php",
		...
	);

PHPMailerSender makes it possible to use external SMTP server, it can be configured like this:

	$CONFIGURATION = array(
		"mail_smtp" => array(
			"host" => MAIL_SERVER_HOST,
			"username" => USERNAME,
			"password" => PASSWORD,
			"secure" => SECURE_METHOD // optional, values "tls" or "ssl"
		)
		...
	);

The option "secure" defines whether mail sending is done via TLS (value "tls") or SSL (value "ssl"), leave out to use non-secured connection.