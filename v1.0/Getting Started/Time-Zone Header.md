---
title: "Time-Zone Header"
excerpt: "Sending data from a different timezone? No problem."
---
[block:callout]
{
  "type": "warning",
  "title": "This is a Version 2.0 feature only.",
  "body": "We're in the process of updating documentation to match V2 of Cachet, which is soon to be released. It clears up inconsistencies in the API and adds a couple of features, remaining backwards compatible."
}
[/block]
You can supply a `Time-Zone` header which defines a timezone according to the list of names from the [Olson database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).

Supplying this header means that we will generate a timestamp for the moment your API call is made in the timezone this header defines. This header will determine the timezone used for generating that current timestamp, rather than using the UTC format.