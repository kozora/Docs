---
title: "Developing Cachet"
excerpt: ""
---
The easiest way to get started developing Cachet is to use [Laravel Homestead](http://laravel.com/docs/5.1/homestead). It comes with everything that you'll need, but if you choose not to use it, then you'll need:

1. Apache or Nginx web server
2. MySQL/Postgres SQL
3. Node.js

Cachet is built upon the [Laravel](http://laravel.com) framework. If this is your first time using Laravel, then you should check its documentation.

Unlike a default Laravel installation, we've moved our models into the `./app/Models` directory. We've also moved a lot of the configuration settings into `.env`.

Most of the leg work is done using the Command Bus. This allows us to share code between the dashboard and the API. Command code is shared between `./app/Commands` and `./app/Handlers/Commands`.