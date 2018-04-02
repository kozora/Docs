---
title: "Post Parameters"
excerpt: ""
---
The API can also take post parameters instead of JSON. When suppling these parameters, you need to set the `Content-type` header to `application/x-www-form-urlencoded`. This is accomplished using the standard `-d` or `--data` flags in curl.
[block:code]
{
  "codes": [
    {
      "code": "curl -u email:password https://demo.cachethq.io/api/resource -X POST -d \"key=value\"",
      "language": "shell"
    }
  ]
}
[/block]