---
title: "Configuring Mail"
excerpt: ""
---
Your `.env` file will need to include the following setting keys.
[block:code]
{
  "codes": [
    {
      "code": "MAIL_DRIVER=smtp\nMAIL_HOST=mailtrap.io\nMAIL_PORT=587\nMAIL_USERNAME=null\nMAIL_PASSWORD=null\nMAIL_ADDRESS=null\nMAIL_NAME=null\nMAIL_ENCRYPTION=tls",
      "language": "text"
    }
  ]
}
[/block]
After making changes to your mail configuration you'll need to run the following command within your Cachet installation directory.
[block:code]
{
  "codes": [
    {
      "code": "$ php artisan config:cache\n\n# If you experience any issues after running this command, run this too:\n$ rm -rf bootstrap/cache/*",
      "language": "shell"
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Cachet + Mailgun"
}
[/block]
Create an account with [Mailgun](https://mailgun.com).

MAIL_USERNAME should be Mailgun domain.
MAIL_PASSWORD should be Mailgun API Key.

Edit your `.env` file with the following variables.
[block:code]
{
  "codes": [
    {
      "code": "MAIL_DRIVER=mailgun\nMAIL_HOST=smtp.mailgun.org\nMAIL_PORT=587\nMAIL_USERNAME=alt-three.com\nMAIL_PASSWORD=xxxx\nMAIL_ADDRESS=support@alt-three.com\nMAIL_NAME=\"Alt Three Services Limited\"\nMAIL_ENCRYPTION=tls",
      "language": "text"
    }
  ]
}
[/block]
The `tls` encryption setting is required to have e-mails be properly delivered.
[block:api-header]
{
  "type": "basic",
  "title": "Cachet + Spark Post"
}
[/block]
Create an account with [Spark Post](https://www.sparkpost.com/).

Edit your `.env` file with the following variables.
[block:code]
{
  "codes": [
    {
      "code": "MAIL_DRIVER=smtp\nMAIL_HOST=smtp.sparkpostmail.com\nMAIL_PORT=587\nMAIL_USERNAME=SMTP_Injection\nMAIL_PASSWORD=API_TOKEN\nMAIL_ADDRESS=support@alt-three.com\nMAIL_NAME=\"Alt Three Services Limited\"\nMAIL_ENCRYPTION=tls",
      "language": "text"
    }
  ]
}
[/block]