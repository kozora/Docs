---
title: "Incident Statuses"
excerpt: ""
---
Cachet uses a zero-based numbering scheme to identify incident statuses. When creating or updating an incident, it's important that you specify the `status` of the incident.

A status can be one of the following values:
[block:parameters]
{
  "data": {
    "h-0": "Status",
    "h-1": "Name",
    "0-0": "`0`",
    "0-1": "Scheduled",
    "1-0": "`1`",
    "1-1": "Investigating",
    "2-0": "`2`",
    "2-1": "Identified",
    "3-0": "`3`",
    "3-1": "Watching",
    "4-0": "`4`",
    "4-1": "Fixed",
    "h-2": "Description",
    "0-2": "This status is *reserved* for a scheduled status.",
    "1-2": "You have reports of a problem and you're currently looking into them.",
    "2-2": "You've found the issue and you're working on a fix.",
    "3-2": "You've since deployed a fix and you're currently watching the situation.",
    "4-2": "The fix has worked, you're happy to close the incident."
  },
  "cols": 3,
  "rows": 5
}
[/block]