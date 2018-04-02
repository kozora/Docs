---
title: "CORS"
excerpt: "Cross-original resource sharing"
---
[block:callout]
{
  "type": "info",
  "title": "External Access",
  "body": "By default Cachet can be **accessed by any** third-party server."
}
[/block]
You may configure your Cachet installation for [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing) very easily. To blacklist everybody except one or more domains:

1. Login to your Dashboard
2. Go to the **Settings** panel
3. Click on **Security** 
4. You'll see a **Allowed domains** textarea, fill in any domains that you want to access the API as a comma separated list:
[block:code]
{
  "codes": [
    {
      "code": "https://demo.cachethq.io,https://status.cachethq.io",
      "language": "text",
      "name": null
    }
  ]
}
[/block]