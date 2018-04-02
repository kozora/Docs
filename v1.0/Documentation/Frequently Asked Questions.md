---
title: "Frequently Asked Questions"
excerpt: "Answers to questions that we're most frequently asked."
---
[block:api-header]
{
  "type": "basic",
  "title": "Do you provide installations?"
}
[/block]
We provide paid support. Please contact us at [support@alt-three.com](mailto:support@alt-three.com?subject=Cachet Installation) with your requirements for more information!
[block:api-header]
{
  "type": "basic",
  "title": "How do I reset a forgotten password?"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "$ cd /var/www/ # the root of your Cachet installation\n$ php artisan tinker\nPsy Shell v0.8.8 (PHP 7.1.6 — cli) by Justin Hileman\n>>> $user = CachetHQ\\Cachet\\Models\\User::find(1);\n=> CachetHQ\\Cachet\\Models\\User {#865\n    id: 1,\n    username: \"test\",\n    email: \"test@test.com\",\n    api_key: \"9yMHsdioQosnyVK4iCVR\",\n    active: 1,\n    level: 1,\n    created_at: \"2015-07-24 13:42:10\",\n    updated_at: \"2015-07-28 15:12:55\",\n}\n>>> $user->update(['password' => 'New Password']);\n\\q\nExit:  Goodbye.",
      "language": "shell",
      "name": null
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "MySQL Permissions"
}
[/block]
Cachet requires a somewhat broad set of permissions to aid installation and setup. For any MySQL user that you use for Cachet, you'll need to provide the following permissions:

1. `CREATE`
2. `ALTER`
3. `SELECT`
4. `INSERT`
5. `UPDATE`
6. `DELETE`
[block:api-header]
{
  "type": "basic",
  "title": "Do you sell any merchandise?"
}
[/block]
We currently have a few stickers! https://cachethq.io/merchandise
[block:api-header]
{
  "type": "basic",
  "title": "Can I donate?"
}
[/block]
You sure can! Visit [https://cachethq.io/donate](https://cachethq.io/donate) or if you'd like to use Paypal, our address is support@alt-three.com