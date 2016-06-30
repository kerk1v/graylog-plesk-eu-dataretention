# Instructions, quick and simple:

1. Login to your plesk server
2. Add the following line at the end of /etc/rsyslog.conf:
   mail.* @<IP_OF_YOUR_GRAYLOG_SERVER>:12320
3. Restart rsyslogd wih the command: 
   service rsyslog restart
4. Import the content pack in this directory into Graylog (tested with 2.0.1).

## For Roundcube logging: 

1. Edit /usr/share/psa-roundcube/config/config.inc.php, add lines: 
      $config['log_driver'] = 'syslog';
      $config['log_session_id'] = 8;
      $config['syslog_id'] = 'roundcube';
      $config['syslog_facility'] = LOG_MAIL;
      $config['log_logins'] = true;
2. Edit /etc/psa-webmail/roundcube/php.ini, add line: 
      date.timezone = "Europe/Madrid"
or whetever your timezone is (see http://php.net/manual/en/timezones.php for a list of timezones)

This will send Roundcube Login / Logoff events to local syslog mail.* which is already forwarded to Graylog (Above!)

### Changes will be overwritten by Plesk updates, check them afterwards

All messages relevant to SMTP incoming and outgoing mail will be identified with the field EU_mail:true

New Release 30/06/15: added extractors to also cover IMAP logins

Work in progress: add Roundcube Webmail logins, sucessful and failed

Enjoy!
