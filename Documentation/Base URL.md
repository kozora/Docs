---
title: "Base URL"
excerpt: ""
---
All API requests have a base URL of:
[block:code]
{
  "codes": [
    {
      "code": "https://example.com/api/v1/",
      "language": "text"
    }
  ]
}
[/block]
The connection may be HTTP if you're not running Cachet with SSL.

The demo page uses `https://demo.cachethq.io/api/v1` as the base URL.
[block:callout]
{
  "type": "info",
  "title": "Don't forget to use your own URL!",
  "body": "The URL provided above is an example domain, you **must** provide your own when running requests."
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Versioning"
}
[/block]
Cachet's API is currently at version `1`. This is represented by the `v1` section in the Base URL.

This means that the API will only gain new features and ideally, nothing should change. A change may only occur if a bug is introduced between minor versions.
[block:callout]
{
  "type": "danger",
  "title": "Cachet vs API Version",
  "body": "API versions do not match the version of Cachet you're using."
}
[/block]