---
title: "Installing Cachet"
excerpt: ""
---
Cachet is constantly evolving therefore, we advise you to always download and use the [latest tagged](https://github.com/CachetHQ/Cachet/releases/latest) release.
[block:callout]
{
  "type": "warning",
  "body": "Using a non-tagged release or the `master` branch may result in an unstable or broken environment.",
  "title": "Warning!"
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Download the source code with Git"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Check out the latest version!",
  "body": "The tags below are examples of what will be shown. You should always run `git checkout` on the latest tag."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "$ cd /var/www # Or wherever you chose to install web applications to\n$ git clone https://github.com/cachethq/Cachet.git\n$ cd Cachet\n$ git tag -l\n\nv0.1.0-alpha\nv1.0.0\nv1.1.0\nv2.0.0\nv2.1.0\n\n$ git checkout v2.1.0",
      "language": "shell"
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Configuring a database"
}
[/block]
By default Cachet comes with a `.env.example` file. You'll need to rename this file to just `.env` **regardless** of what environment you're working on.

It's now just a case of editing this new `.env` file and setting the values of your setup.
[block:callout]
{
  "type": "info",
  "title": "Environment Configuration Notice",
  "body": "Any values with spaces in them should be contained within double quotes."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "APP_ENV=production\nAPP_DEBUG=false\nAPP_URL=http://localhost\nAPP_KEY=SomeRandomString\n\nDB_DRIVER=mysql\nDB_HOST=localhost\nDB_DATABASE=cachet\nDB_USERNAME=homestead\nDB_PASSWORD=secret\nDB_PORT=null\n\nCACHE_DRIVER=apc\nSESSION_DRIVER=apc\nQUEUE_DRIVER=sync\nCACHET_EMOJI=false\n\nMAIL_DRIVER=smtp\nMAIL_HOST=mailtrap.io\nMAIL_PORT=2525\nMAIL_USERNAME=null\nMAIL_PASSWORD=null\nMAIL_ADDRESS=null\nMAIL_NAME=\"Demo Status Page\"\nMAIL_ENCRYPTION=tls\n\nREDIS_HOST=null\nREDIS_DATABASE=null\nREDIS_PORT=null\n\nGITHUB_TOKEN=null\n",
      "language": "text",
      "name": null
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "body": "If you're using SQLite then your `.env` file should not contain a `DB_HOST` key. You'll also need to `touch ./database/database.sqlite` and give it the required permissions.",
  "title": "SQLite hosts"
}
[/block]
## Install Composer

`curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer`
[block:code]
{
  "codes": [
    {
      "code": "$ composer install --no-dev -o",
      "language": "shell"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Struggling with Composer?",
  "body": "If you're stuck at the Composer stage, you can run `composer install --no-dev -o --no-scripts` which usually fixes any issues on Windows servers."
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Set the application key"
}
[/block]
Before going any further, we need to set the `APP_KEY` config. This is used for all encryption used in Cachet.
[block:code]
{
  "codes": [
    {
      "code": "$ php artisan key:generate",
      "language": "shell"
    }
  ]
}
[/block]
Be sure that you have the right permissions to .env before running this command. 
[block:api-header]
{
  "type": "basic",
  "title": "Using the install command"
}
[/block]
Cachet comes with an installation command that will:

- Run migrations
- Run seeders (of which there are none)
[block:code]
{
  "codes": [
    {
      "code": "$ php artisan app:install\t",
      "language": "shell"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "danger",
  "body": "Never change the `APP_KEY` after installation on production environment. This will result in all of your encrypted/hashed data being lost."
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "Getting a 500 - Internal Server Error?",
  "body": "If you get a 500 error when visiting your status page, you may need to run `chmod -R 777 storage` for it to work or `rm -rf bootstrap/cache/*`"
}
[/block]
You can also try to give permissions to cache `chmod -R 777 bootstrap/`
[block:api-header]
{
  "type": "basic",
  "title": "Running Cachet on Apache"
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "Required Apache Modules",
  "body": "You need to enable `mod_rewrite` for Apache. On Debian-based systems you can do this by\n\n```bash\n# a2enmod rewrite\n```"
}
[/block]
Once Cachet is setup, the Apache installation is as simple as creating a new Virtual Host entry in the `httpd-vhosts.conf` file.
[block:code]
{
  "codes": [
    {
      "code": "<VirtualHost *:80>\n    ServerName cachet.dev \n    # Or whatever you want to use\n    ServerAlias cachet.dev \n    # Make this the same as ServerName\n    DocumentRoot \"/var/www/Cachet/public\"\n    <Directory \"/var/www/Cachet/public\">\n        Require all granted \n        # Used by Apache 2.4\n        Options Indexes FollowSymLinks\n        AllowOverride All\n        Order allow,deny\n        Allow from all\n    </Directory>\n</VirtualHost>",
      "language": "text"
    }
  ]
}
[/block]
Restart Apache by running the following:
[block:code]
{
  "codes": [
    {
      "code": "$ sudo service apache2 restart",
      "language": "shell"
    }
  ]
}
[/block]
If you also need HTTPS on apache you will need to get the ssl mod installed and the default ssl conf file enabled.  See  DigitalOcean's [documentation](https://www.digitalocean.com/community/tutorials/how-to-create-a-ssl-certificate-on-apache-for-ubuntu-14-04). 
[block:api-header]
{
  "type": "basic",
  "title": "Running Cachet on nginx"
}
[/block]
- You'll need to install `php5-fpm` - [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-12-04) has a nice LEMP installation tutorial
- Generate your SSL key+certificate
- Create a new vhost such as `/etc/nginx/sites-enabled/cachet.conf`:
[block:code]
{
  "codes": [
    {
      "code": "# Upstream to abstract backend connection(s) for php\nupstream php {\n    server unix:/tmp/php-cgi.socket;\n    server 127.0.0.1:9000;\n}\n\nserver {\n    server_name  cachet.mycompany.com; # Or whatever you want to use\n    listen 80 default;\n    rewrite ^(.*) https://cachet.mycompany.com$1 permanent;\n}\n\n# HTTPS server\n\nserver {\n    listen 443;\n    server_name cachet.mycompany.com;\n\n    root /var/vhost/cachet.mycompany.com/public;\n    index index.php;\n\n    ssl on;\n    ssl_certificate /etc/ssl/crt/cachet.mycompany.com.crt; # Or wherever your crt is\n    ssl_certificate_key /etc/ssl/key/cachet.mycompany.com.key; # Or wherever your key is\n    ssl_session_timeout 5m;\n\n    # Best practice as at March 2014\n    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;\n    ssl_prefer_server_ciphers on;\n    ssl_ciphers \"ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA\";\n    ssl_buffer_size 1400; # 1400 bytes, within MTU - because we generally have small responses. Could increase to 4k, but default 16k is too big\n\n    location / {\n        add_header Strict-Transport-Security max-age=15768000;\n        try_files $uri /index.php$is_args$args;\n    }\n\n    location ~ \\.php$ {\n                include fastcgi_params;\n                fastcgi_pass unix:/var/run/php5-fpm.sock;\n                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;\n                fastcgi_index index.php;\n                fastcgi_keep_conn on;\n                add_header Strict-Transport-Security max-age=15768000;\n    }\n}",
      "language": "text"
    }
  ]
}
[/block]
Start `php5-fpm` and `nginx` and you're done!