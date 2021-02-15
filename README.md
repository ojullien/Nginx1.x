# Nginx1.x configuration and templates

Nginx1.x personnal configuration and website templates on Debian linux distribution.

*Note: I use those templates for my own projects, they contain the features I need.*

## Table of Contents

[Requirements](#requirements) | [Configuration](#configuration) | [Templates](#templates) | [Documentation](#documentation) | [Contributing](#contributing) | [License](#license)

## Requirements

- Debian linux distribution: ~10.0
- nginx: ~1.18
- nginx-extra: ~1.18
- openssl: ~1.1.1i

## Configuration

I do not modify any NGINX configuration files. I just add new configuration files to override the default NGINX configuration.

According to the nginx.conf file, when it starts, NGINX includes the module configuration files (/etc/nginx/modules-enabled/\*.conf) and, then, the particular configuration snippets (/etc/nginx/conf.d/\*.conf) which manage global configuration fragments.

### Files

- zzz-apache2.conf: overrides the main Apache server configuration.
- zzz-deflate.conf: overrides the DEFLATE configuration that allows output from your server to be compressed before being sent to the client over the network.
- zzz-dir.conf: overrides the default serving directory index files configuration.
- zzz-evasive.conf: overrides the default EVASIVE module configuration.
- zzz-expires.conf: overrides and extends the default expirations time by type.
- zzz-expires-cdn.conf: modern version for caching while using CDN.
- zzz-expires-fingerprint.conf: modern version for caching while using fingerprinted URLs.
- zzz-headers.conf: adds few HTTP request and response headers customizations.
- zzz-log.conf: overrides log configuration.
- zzz-mime.conf: adds more mime types.
- zzz-mpm_event.conf: overrides the event worker MPM default configuration.
- zzz-php7.x-fpm.conf: configure the local php-fpm using proxy.
- zzz-proxy.conf: overrides the multi-protocol proxy/gateway server default configuration.
- zzz-remoteip.conf: overides remoteip configuration.
- zzz-security.conf: overrides and adds more security configuration snippets for the server.
- zzz-ssl.conf: SSL configuration.
- zzz-status.conf: overrides the status and info modules configurations.

### How to setup the Apache2.4 personnal configuration

1. Copy the configuration [files](/src/conf-available) into /etc/apache2/conf-available
2. Edit the named like zzz-***.conf files and make changes as you need.
3. Enable the configuration you need using `a2enconf zzz-***`
4. Test the configuration using `apache2ctl -t`
5. When test is OK, activate the new configuration using `systemctl reload apache2`

## Templates

I wrote theses templates to ease the process of creating Server Blocks.

I do not use the module mod_macro, I only use the built-in Include and Define directives.

Each domain.tld directory contains configuration for HTTP and HTTPS. The domain.tld/include contains the common snippets for HTTP and HTTPS.

The Content Security Policy (CSP) snippets depends on your site and must be tested.

Module mod_http2 must be enable to provides HTTP/2 support in SSL.

### Features

- shared: contains many files with common snippets.
  - **access_control directory** contains Access control directives for application and static website.
  - **security directory** contains security directives for HSTS and WordPress.
- 000-default: contains the default Server Blocks configuration.
- static.tld: contains the name-based vhost configuration for a static website.
- app.tld: contains the name-based vhost configuration for a PHP application.
- api.tld: contains the name-based vhost configuration for a mixed static website and PHP application.
- redirect.tld: contains the configuration for a redirection.
- reverseproxy.tld: configuration sample for a reverse proxy.
  - **remoteip_module**, **proxy_module** and **proxy_http_module** or/and **proxy_http2_module** are required.
  - **conf-available/zzz-expires.conf** and **conf-available/zzz-headers.conf** should not be enabled.
- loader.conf: one file to rule them all.

### How to setup the site templates

1. Copy the [templates](/src/sites-available) into /etc/apache2/sites-available
2. Edit the files and make changes as you need.
3. Edit and update the loader.conf file.
4. Enable the sites using `a2ensite loader`
5. restarts the Apache daemon using `apache2ctl graceful`

## Documentation

I wrote and I use this package for my own projects. And, unfortunately, I do not provide exhaustive documentation. Please read the code and the comments ;)

For instructions on how to use, best practices, templates and other usage information, please visit the [NGINX documentation](https://nginx.org/en/docs/).

## Contributing

Thanks you for taking the time to contribute. Please fork the repository and make changes as you'd like.

As I use these configuration and templates for my own projects, it contains only the features I need. But If you have any ideas, just open an [issue](https://github.com/ojullien/Nginx1.x/issues) and tell me what you think. Pull requests are also warmly welcome.

If you encounter any **bugs** in the configuration or templates, please open an [issue](https://github.com/ojullien/Nginx1.x/issues).

Be sure to include a title and clear description,as much relevant information as possible, and a code sample or an executable test case demonstrating the expected behavior that is not occurring.

## License

**Nginx1.x configuration and templates** are open-source and are licensed under the [BSD 2-Clause License](https://github.com/ojullien/Nginx1.x/blob/master/LICENSE).
