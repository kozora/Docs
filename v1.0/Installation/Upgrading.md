---
title: "Upgrading"
excerpt: ""
---
If you've installed Cachet using Git, then upgrading should be straight forward, requiring just a few minutes.
[block:callout]
{
  "type": "success",
  "title": "Before you get started, backup!",
  "body": "Make sure that you've taken a **backup of your Cachet database**. We test thoroughly, but you never know.\n\n**Cachet v2.3 will automatically backup your database for Postgres and MySQL installations only.**"
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Maintenance mode"
}
[/block]
Before we go any further, it's good practice to put your status page into maintenance mode. This will simply show a "Maintenance" page until the updates have completed.
[block:code]
{
  "codes": [
    {
      "code": "$ php artisan down",
      "language": "shell"
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Fetch the latest code"
}
[/block]
Upgrading with Git is very easy:
[block:code]
{
  "codes": [
    {
      "code": "$ git fetch origin\n$ git tag -l\n$ git checkout LATEST_TAG",
      "language": "shell"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "LATEST_TAG?",
  "body": "Checking out a `LATEST_TAG` value won't work. You need to replace this with the latest version from the output of `git tag -l`."
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Upgrading dependencies"
}
[/block]
Next, we need to upgrade our dependencies. These usually contain bug fixes, performance enhancements, and new features.
[block:code]
{
  "codes": [
    {
      "code": "$ composer install --no-dev -o --no-scripts",
      "language": "shell"
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Update the app!"
}
[/block]
We now need to ask Cachet to run any migrations, upgrade paths, and clean up anything that is no longer needed.
[block:code]
{
  "codes": [
    {
      "code": "$ php artisan app:update",
      "language": "shell"
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Starting the app again!"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "$ php artisan up",
      "language": "shell"
    }
  ]
}
[/block]
If you don't start it again you will get a 500 error too!
[block:api-header]
{
  "type": "basic",
  "title": "Experienced any issues?"
}
[/block]
If you experience any issues when running these commands, you may need to execute the following command:
[block:code]
{
  "codes": [
    {
      "code": "$ rm -rf bootstrap/cache/*",
      "language": "shell"
    }
  ]
}
[/block]
You may also want to try restoring from the backup you took earlier.