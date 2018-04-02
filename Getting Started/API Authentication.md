---
title: "API Authentication"
excerpt: "Authenticating your protected API requests."
---
Cachet is built on the belief that your service status is open and transparent, therefore all `GET` requests are public and require no authentication to access the information. The following are exempt from this rule:

- Disabled components will only return in the Component API if you provide a valid API token.
- The Subscribers API will only work if you provide a valid API token, we don't want to expose email addresses.

All other requests require authentication, either with **Basic Auth** or the preferred **API Token**.
[block:api-header]
{
  "type": "basic",
  "title": "BasicAuth"
}
[/block]
When making any request to the API which is not a `GET`, you'll need to use some kind of authentication. The simplest of the authorization methods offered by Cachet is [BasicAuth](http://en.wikipedia.org/wiki/Basic_access_authentication).
[block:callout]
{
  "type": "danger",
  "title": "This is not secure",
  "body": "For obvious reasons, sending your authentication details in plain text is not secure. We do advise that you add SSL to your Cachet installation for added security, but suggest using API tokens."
}
[/block]
To authenticate your requests you only need to provide your email and password.
[block:code]
{
  "codes": [
    {
      "code": "$ curl -u username@example.com:password -H \"Content-Type: application/json\" -d '{\"name\":\"API\",\"description\":\"An example description\",\"status\":1}' http://status.cachethq.io/api/v1/components",
      "language": "shell"
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "API Token"
}
[/block]
The API Token is generated at installation time for the main user or when a new team member is added to your status page and can be found on your profile page (click your profile picture to get there).

Once you have your token you'll need to add a new request header of `X-Cachet-Token: TOKEN`
[block:code]
{
  "codes": [
    {
      "code": "$ curl -H \"Content-Type: application/json;\" -H \"X-Cachet-Token: YOUR_KEY_HERE\" -d '{\"name\":\"API\",\"description\":\"An example description\",\"status\":1}' http://status.cachethq.io/api/v1/components",
      "language": "shell"
    }
  ]
}
[/block]