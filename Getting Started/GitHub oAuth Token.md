---
title: "GitHub oAuth Token"
excerpt: ""
---
[block:callout]
{
  "type": "info",
  "title": "Emoji support is turned off by default!",
  "body": "To enable Emoji you'll need to modify your `.env` file and add `CACHET_EMOJI=true`."
}
[/block]
Supporting Emoji codes such as `:smile:` and `:beers:`, is made possible by GitHub's public API.

Under some circumstances it's possible to hit GitHub's API rate limit quickly. This would render your status page inaccessible.

To get around this you can create a GitHub oAuth Token and set it in your `.env` file. Follow these instructions to create and setup Cachet with your token.
[block:api-header]
{
  "type": "basic",
  "title": "To GitHub!"
}
[/block]
Start off by going to your [GitHub Settings page](https://github.com/settings/profile)
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8ceLcQHTQP6yBW2JwQry_Screen%20Shot%202015-08-06%20at%2019.00.35.png",
        "Screen Shot 2015-08-06 at 19.00.35.png",
        "207",
        "278",
        "#467cc3",
        ""
      ]
    }
  ]
}
[/block]
Uses the sidebar to access [Personal access tokens](https://github.com/settings/tokens).
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/OU5t03KRwS9zNwZzw3tF_Screen%20Shot%202015-08-06%20at%2019.02.27.png",
        "Screen Shot 2015-08-06 at 19.02.27.png",
        "249",
        "436",
        "#4e71a3",
        ""
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Generate a new token"
}
[/block]
Click on the **Generate new token** button in the top right of the view.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/Kg26DjuSSd6vBshBsqiC_Screen%20Shot%202015-08-06%20at%2019.03.15.png",
        "Screen Shot 2015-08-06 at 19.03.15.png",
        "740",
        "96",
        "#9e7773",
        ""
      ]
    }
  ]
}
[/block]
Give the token a name, such as: **Cachet GitHub Token**. Then uncheck all scopes except for **User**. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/CuyEPD3oRpGhQL5rc7ZN_Screen%20Shot%202015-08-06%20at%2019.04.54.png",
        "Screen Shot 2015-08-06 at 19.04.54.png",
        "745",
        "528",
        "#a07b69",
        ""
      ]
    }
  ]
}
[/block]
Click **Generate token** and GitHub will take you back to the list of tokens from before. Copy the code into your clipboard.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/qJPlfjQHuyfvybbFjEA0_Screen%20Shot%202015-08-06%20at%2019.05.57.png",
        "Screen Shot 2015-08-06 at 19.05.57.png",
        "741",
        "44",
        "#81a6c0",
        ""
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Put the code in your environment"
}
[/block]
Now you need to edit the `.env` file and add the following (or change the default value if you're a new installation).
[block:code]
{
  "codes": [
    {
      "code": "GITHUB_TOKEN=5c25370fcf7db4a676d98d72700e2922654485ed",
      "language": "text"
    }
  ]
}
[/block]
After changing the configuration you'll now need to run the following:
[block:code]
{
  "codes": [
    {
      "code": "$ php artisan config:cache",
      "language": "shell"
    }
  ]
}
[/block]