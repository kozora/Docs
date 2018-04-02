---
title: "Meta Object"
excerpt: "Additional response information."
---
All `GET` responses contain a meta object. This object is mainly used for paging results.
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"meta\": {\n        \"pagination\": {\n            \"total\": 5,\n            \"count\": 5,\n            \"per_page\": 20,\n            \"current_page\": 1,\n            \"total_pages\": 1,\n            \"links\": {\n                \"next_page\": null,\n                \"previous_page\": null\n            }\n        }\n    }\n}",
      "language": "json"
    }
  ]
}
[/block]