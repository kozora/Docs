---
title: "Configuring the Queue"
excerpt: ""
---
Cachet uses a queue to send [Configuring Mail](doc:configuring-mail) and [Beacons](doc:beacons) without slowing down the rest of the application. This can be setup in a variety of ways.

[block:api-header]
{
  "type": "basic",
  "title": "Supervisor"
}
[/block]
The recommended setup for the queue is to use [Supervisor](https://www.digitalocean.com/community/tutorials/how-to-install-and-manage-supervisor-on-ubuntu-and-debian-vps).

> Supervisor is a process manager which makes managing a number of long-running programs a trivial task by providing a consistent interface through which they can be monitored and controlled.
[block:api-header]
{
  "type": "basic",
  "title": "Installations up to Cachet v2.3"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "[program:cachet-queue]\ncommand=php artisan queue:work --daemon --delay=2 --sleep=1 --tries=3\ndirectory=/var/www/cachet/\nredirect_stderr=true\nautostart=true\nautorestart=true\nuser=cachet",
      "language": "text",
      "name": "cachet.conf"
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Installations from Cachet v2.4-dev onwards"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "[program:cachet-queue]\ncommand=php artisan queue:work --delay=1 --sleep=1 --timeout=1800 --tries=3\ndirectory=/var/www/cachet/\nredirect_stderr=true\nautostart=true\nautorestart=true\nuser=cachet",
      "language": "text",
      "name": "cachet.conf"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Update to your configuration!",
  "body": "Be sure to update the values in the example configuration above to match your installation setup."
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Database Queue with Cron"
}
[/block]
The default installation of Cachet sets the queue type to `database` which means that all jobs are stored within your database and is then processed by a cron job which calls an artisan command from within the project directory.

You'll need to create a new cron job, in Ubuntu it's a case of running `crontab -e` and adding this line:
[block:code]
{
  "codes": [
    {
      "code": "* * * * * php /path/to/artisan schedule:run >> /dev/null 2>&1",
      "language": "text"
    }
  ]
}
[/block]
Close the file and the cron job will now begin running, processing any confirmation and incident emails.
[block:api-header]
{
  "type": "basic",
  "title": "Synchronous Queue (not recommended for larger installs)"
}
[/block]
If you cannot add a queue job, another alternative is to process all of the *jobs* immediately after they are created.
[block:callout]
{
  "type": "warning",
  "title": "Not suitable for larger installations!",
  "body": "This setup is not ideal for larger installs with hundreds of subscribers as each email can take a few seconds to send and would slow down your interaction with the system."
}
[/block]
To set this up change the `.env` file with the following setting:
[block:code]
{
  "codes": [
    {
      "code": "QUEUE_DRIVER=sync",
      "language": "text"
    }
  ]
}
[/block]