---
title: "Installing Cachet on Windows"
excerpt: "This is the Windows specific installation manual."
---
Cachet is constantly evolving, therefore we advise you to download and checkout the latest tagged release.

Using a branch, especially `master` could result in a broken or unstable environment.
[block:api-header]
{
  "type": "basic",
  "title": "Download the source code with Git"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "$ cd /var/www\n$ git clone https://github.com/cachethq/Cachet.git\n$ cd Cachet\n$ git tag -l\n\nv0.1.0-alpha\nv1.0.0\nv1.1.0\n\n$ git checkout v1.1.0",
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
By default Cachet comes with a `.env.example` file. You'll need to rename this file to just `.env` **regardless** of what environment you're working on. This is how Laravel 5 deals with configurations.

It's now just a case of editing this new `.env` file and setting the values of your setup.

Here is an example Windows  file with a MySQL database:


[block:code]
{
  "codes": [
    {
      "code": "APP_ENV=production\nAPP_DEBUG=false\nAPP_URL=http://localhost\nAPP_KEY=SomeRandomString\n\nDB_DRIVER=mysql\nDB_HOST=localhost\nDB_DATABASE=cachet\nDB_USERNAME=homestead\nDB_PASSWORD=secret\nDB_PORT=null\n\nCACHE_DRIVER=file\nSESSION_DRIVER=file\nQUEUE_DRIVER=database\nCACHET_EMOJI=false\n\nMAIL_DRIVER=smtp\nMAIL_HOST=mailtrap.io\nMAIL_PORT=2525\nMAIL_USERNAME=null\nMAIL_PASSWORD=null\nMAIL_ADDRESS=null\nMAIL_NAME=null\nMAIL_ENCRYPTION=tls\n\nREDIS_HOST=null\nREDIS_DATABASE=null\nREDIS_PORT=null\n\nGITHUB_TOKEN=null\n",
      "language": "text",
      "name": ".env"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "SQLite Hosts",
  "body": "If you're using SQLite then your `.env` file should not contain a `DB_HOST` key. You'll also need to `touch ./database/database.sqlite` and give it the required permissions."
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Debug Mode",
  "body": "After the install, don't forget to set `APP_DEBUG` to false to avoid other people to see your application info!"
}
[/block]

[block:callout]
{
  "type": "danger",
  "title": "Subscribers Configuration",
  "body": "The above `.env` file is configured for `Synchronous Queue` for subscriber emails. This may not be suitable for your configuration so it is very important you also read the [Configuring Subscribers](https://docs.cachethq.io/docs/setup-subscribers) section of the docs and change your `.env` as required."
}
[/block]
Now, in your Command Prompt, navigate to your Cachet install and run:
[block:code]
{
  "codes": [
    {
      "code": "composer install --no-dev -o",
      "language": "shell"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Struggling With Composer?",
  "body": "Composer sometimes has errors when trying to install scripts. Windows users should use this command if you get errors after running the above command."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "composer install --no-dev -o --no-scripts",
      "language": "shell"
    }
  ]
}
[/block]
Once we've decided on our database, we now need to run the migrations to create the tables. In our command line we need to run the migrations, from within the root directory:

You should see the output of the current project migration files being migrated to your database.
[block:api-header]
{
  "type": "basic",
  "title": "Security Key"
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

[block:api-header]
{
  "type": "basic",
  "title": "Installing Cachet"
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
  "body": "Never change the `APP_KEY` after installation on production environment. All your encrypted / hashed data will be lost, becoming unusable!"
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "PHP.ini Config"
}
[/block]
Some extensions need to be uncommented in your `php.ini` file. This are the extensions I have enabled and disabled, however it may vary with your PHP install.


[block:code]
{
  "codes": [
    {
      "code": "extension=php_apcu.dll\nextension=php_bz2.dll\nextension=php_curl.dll\nextension=php_mbstring.dll\nextension=php_exif.dll\n;extension=php_fileinfo.dll\nextension=php_gd2.dll\nextension=php_gettext.dll\n;extension=php_gmp.dll\nextension=php_intl.dll\nextension=php_imap.dll\n;extension=php_interbase.dll\n;extension=php_ldap.dll\n;extension=php_mssql.dll\n;extension=php_mbstring.dll\n;extension=php_exif.dll      ; Must be after mbstring as it depends on it\nextension=php_mysql.dll\nextension=php_mysqli.dll\n;extension=php_oci8.dll      ; Use with Oracle 10gR2 Instant Client\n;extension=php_oci8_11g.dll  ; Use with Oracle 11gR2 Instant Client\n\n\nextension=php_openssl.dll\n;extension=php_pdo_firebird.dll\nextension=php_pdo_mysql.dll\n;extension=php_pdo_oci.dll\n;extension=php_pdo_odbc.dll\n;extension=php_pdo_pgsql.dll\nextension=php_pdo_sqlite.dll\n;extension=php_pdo_sqlite_external.dll\n;extension=php_pgsql.dll\n;extension=php_pspell.dll\n;extension=php_shmop.dll\n\n; The MIBS data available in the PHP distribution must be installed. \n; See http://www.php.net/manual/en/snmp.installation.php \n;extension=php_snmp.dll\n\nextension=php_soap.dll\nextension=php_sockets.dll\nextension=php_sqlite3.dll\n;extension=php_sybase_ct.dll\n;extension=php_tidy.dll\nextension=php_xmlrpc.dll\nextension=php_xsl.dll\n",
      "language": "php",
      "name": "php.ini"
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Apache vHosts"
}
[/block]
Apache is one of the easier installations. We simply need to create a new Virtual Host and add it to our `HOSTS` file.

To do this, we simply add the following Virtual Host to our `httpd-vhosts.conf` file. Do change this to suit your setup:

[block:code]
{
  "codes": [
    {
      "code": "<VirtualHost *:80>\n    ServerAdmin **Intentionally Hidden**\n    DocumentRoot \"C:\\Users\\Administrator\\Desktop\\Cachet\\public\"\n    ServerName status.theobearman.com\n</VirtualHost>",
      "language": "text",
      "name": "httpd-vhosts.conf"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "danger",
  "title": "You Need to Enable `mod_rewrite` for Apache.",
  "body": "You can do this by finding your `httpd.conf` file and uncommenting the following line:\n\n`#LoadModule rewrite_module modules/mod_rewrite.so`"
}
[/block]
The rest of the contents of my `httpd.conf` file are as follows:
[block:code]
{
  "codes": [
    {
      "code": "LoadModule access_compat_module modules/mod_access_compat.so\nLoadModule actions_module modules/mod_actions.so\nLoadModule alias_module modules/mod_alias.so\nLoadModule allowmethods_module modules/mod_allowmethods.so\nLoadModule asis_module modules/mod_asis.so\nLoadModule auth_basic_module modules/mod_auth_basic.so\n#LoadModule auth_digest_module modules/mod_auth_digest.so\n#LoadModule auth_form_module modules/mod_auth_form.so\n#LoadModule authn_anon_module modules/mod_authn_anon.so\nLoadModule authn_core_module modules/mod_authn_core.so\n#LoadModule authn_dbd_module modules/mod_authn_dbd.so\n#LoadModule authn_dbm_module modules/mod_authn_dbm.so\nLoadModule authn_file_module modules/mod_authn_file.so\n#LoadModule authn_socache_module modules/mod_authn_socache.so\n#LoadModule authnz_fcgi_module modules/mod_authnz_fcgi.so\n#LoadModule authnz_ldap_module modules/mod_authnz_ldap.so\nLoadModule authz_core_module modules/mod_authz_core.so\n#LoadModule authz_dbd_module modules/mod_authz_dbd.so\n#LoadModule authz_dbm_module modules/mod_authz_dbm.so\nLoadModule authz_groupfile_module modules/mod_authz_groupfile.so\nLoadModule authz_host_module modules/mod_authz_host.so\n#LoadModule authz_owner_module modules/mod_authz_owner.so\nLoadModule authz_user_module modules/mod_authz_user.so\nLoadModule autoindex_module modules/mod_autoindex.so\n#LoadModule buffer_module modules/mod_buffer.so\n#LoadModule cache_module modules/mod_cache.so\n#LoadModule cache_disk_module modules/mod_cache_disk.so\n#LoadModule cache_socache_module modules/mod_cache_socache.so\n#LoadModule cern_meta_module modules/mod_cern_meta.so\nLoadModule cgi_module modules/mod_cgi.so\n#LoadModule charset_lite_module modules/mod_charset_lite.so\n#LoadModule data_module modules/mod_data.so\n#LoadModule dav_module modules/mod_dav.so\n#LoadModule dav_fs_module modules/mod_dav_fs.so\nLoadModule dav_lock_module modules/mod_dav_lock.so\n#LoadModule dbd_module modules/mod_dbd.so\n#LoadModule deflate_module modules/mod_deflate.so\nLoadModule dir_module modules/mod_dir.so\n#LoadModule dumpio_module modules/mod_dumpio.so\nLoadModule env_module modules/mod_env.so\n#LoadModule expires_module modules/mod_expires.so\n#LoadModule ext_filter_module modules/mod_ext_filter.so\n#LoadModule file_cache_module modules/mod_file_cache.so\n#LoadModule filter_module modules/mod_filter.so\nLoadModule headers_module modules/mod_headers.so\n#LoadModule heartbeat_module modules/mod_heartbeat.so\n#LoadModule heartmonitor_module modules/mod_heartmonitor.so\n#LoadModule ident_module modules/mod_ident.so\n#LoadModule imagemap_module modules/mod_imagemap.so\nLoadModule include_module modules/mod_include.so\nLoadModule info_module modules/mod_info.so\nLoadModule isapi_module modules/mod_isapi.so\n#LoadModule lbmethod_bybusyness_module modules/mod_lbmethod_bybusyness.so\n#LoadModule lbmethod_byrequests_module modules/mod_lbmethod_byrequests.so\n#LoadModule lbmethod_bytraffic_module modules/mod_lbmethod_bytraffic.so\n#LoadModule lbmethod_heartbeat_module modules/mod_lbmethod_heartbeat.so\n#LoadModule ldap_module modules/mod_ldap.so\n#LoadModule logio_module modules/mod_logio.so\nLoadModule log_config_module modules/mod_log_config.so\n#LoadModule log_debug_module modules/mod_log_debug.so\n#LoadModule log_forensic_module modules/mod_log_forensic.so\n#LoadModule lua_module modules/mod_lua.so\nLoadModule cache_disk_module modules/mod_cache_disk.so\n#LoadModule macro_module modules/mod_macro.so\nLoadModule mime_module modules/mod_mime.so\n#LoadModule mime_magic_module modules/mod_mime_magic.so\nLoadModule negotiation_module modules/mod_negotiation.so\nLoadModule proxy_module modules/mod_proxy.so\n#LoadModule proxy_ajp_module modules/mod_proxy_ajp.so\n#LoadModule proxy_balancer_module modules/mod_proxy_balancer.so\n#LoadModule proxy_connect_module modules/mod_proxy_connect.so\n#LoadModule proxy_express_module modules/mod_proxy_express.so\n#LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so\n#LoadModule proxy_ftp_module modules/mod_proxy_ftp.so\nLoadModule proxy_html_module modules/mod_proxy_html.so\nLoadModule proxy_http_module modules/mod_proxy_http.so\n#LoadModule proxy_scgi_module modules/mod_proxy_scgi.so\n#LoadModule proxy_wstunnel_module modules/mod_proxy_wstunnel.so\n#LoadModule ratelimit_module modules/mod_ratelimit.so\n#LoadModule reflector_module modules/mod_reflector.so\n#LoadModule remoteip_module modules/mod_remoteip.so\n#LoadModule request_module modules/mod_request.so\n#LoadModule reqtimeout_module modules/mod_reqtimeout.so\nLoadModule rewrite_module modules/mod_rewrite.so\n#LoadModule sed_module modules/mod_sed.so\n#LoadModule session_module modules/mod_session.so\n#LoadModule session_cookie_module modules/mod_session_cookie.so\n#LoadModule session_crypto_module modules/mod_session_crypto.so\n#LoadModule session_dbd_module modules/mod_session_dbd.so\nLoadModule setenvif_module modules/mod_setenvif.so\n#LoadModule slotmem_plain_module modules/mod_slotmem_plain.so\n#LoadModule slotmem_shm_module modules/mod_slotmem_shm.so\n#LoadModule socache_dbm_module modules/mod_socache_dbm.so\n#LoadModule socache_memcache_module modules/mod_socache_memcache.so\nLoadModule socache_shmcb_module modules/mod_socache_shmcb.so\n#LoadModule speling_module modules/mod_speling.so\nLoadModule ssl_module modules/mod_ssl.so\nLoadModule status_module modules/mod_status.so\n#LoadModule substitute_module modules/mod_substitute.so\n#LoadModule unique_id_module modules/mod_unique_id.so\n#LoadModule userdir_module modules/mod_userdir.so\n#LoadModule usertrack_module modules/mod_usertrack.so\nLoadModule version_module modules/mod_version.so\n#LoadModule vhost_alias_module modules/mod_vhost_alias.so\n#LoadModule watchdog_module modules/mod_watchdog.so\n#LoadModule xml2enc_module modules/mod_xml2enc.so",
      "language": "text"
    }
  ]
}
[/block]