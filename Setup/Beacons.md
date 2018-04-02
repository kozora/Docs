---
title: "Beacons"
excerpt: ""
---
[block:callout]
{
  "type": "warning",
  "title": "Version Support",
  "body": "Beacons will be introduced in v2.4.0"
}
[/block]
Cachet will periodically communicate with our remote server. This is done so that we're able to gather information about the current version of Cachet and will later be used for system announcements.
[block:api-header]
{
  "type": "basic",
  "title": "Disabling the beacon"
}
[/block]
To disable the beacon, you can turn off the following setting in your `.env` file.
[block:code]
{
  "codes": [
    {
      "code": "CACHET_BEACON=false",
      "language": "text"
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "What is reported?"
}
[/block]
We report the following information to our server:

- A unique installation ID
- The current version of Cachet
- A support contact email (the first enabled admin's email)
- Anonymous statistics (the number of users, incidents, components and metrics)
[block:callout]
{
  "type": "info",
  "title": "Support Contact Email",
  "body": "The contact email is used for the sole purpose of security announcements and will never be used for anything else."
}
[/block]