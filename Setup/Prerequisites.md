---
title: "Prerequisites"
excerpt: "To start using Cachet, you'll need some prerequisites."
---
[block:api-header]
{
  "type": "basic",
  "title": "Application Prerequisites"
}
[/block]
You'll need at least the following installed on your server:

- PHP 5.5.9, you'll also need `ext-gd`, `ext-simplexml`, `mcrypt` and `ext-xml` installed.
- [Composer](https://getcomposer.org/) and `ext-mbstring`,`ext-tokenizer`
- APC or Redis for caching.
- A database driver for your DB, such as MySQL, PostgreSQL or SQLite.
- [Git](https://git-scm.com)
 
[block:callout]
{
  "type": "info",
  "title": "SQLite",
  "body": "Whilst we support SQLite, we advise not using it for status pages with a high amount of traffic."
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "MySQL Timezone Info",
  "body": "Ensure your MySQL database has been updated with the correct timezone information. This will ensure that metrics are shown correctly: https://dev.mysql.com/doc/refman/5.7/en/time-zone-support.html"
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Developer Prerequisites"
}
[/block]
If you're looking to contribute to Cachet you may need some extra dependencies; depending on what you're looking for.

Our CSS is compiled from SCSS, so to compile this you'll need the following:

- Node.js
- NPM
- Bower
- Gulp