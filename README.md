# Nginx1.x configuration and templates

Nginx1.x personnal configuration and website templates on Debian linux distribution.

*Note: I use those templates for my own projects, they contain the features I need.*

## Table of Contents

[Requirements](#requirements) | [Configuration](#configuration) | [Templates](#templates) | [Documentation](#documentation) | [Contributing](#contributing) | [License](#license)

## Requirements

- Debian linux distribution: ~10.0
- nginx: ~1.18
- openssl: ~1.1.1i

## Configuration

I do not modify any NGINX configuration files. I just add new configuration files to override the default NGINX configuration.

According to the nginx.conf file, when it starts, NGINX includes the module configuration files (/etc/nginx/modules-enabled/\*.conf) and, then, the particular configuration snippets (/etc/nginx/conf.d/\*.conf) which manage global configuration fragments.

### Files

- brotli.conf: configures brotli compression.
- cache.conf: configures the cache.
- dir.conf: defines files that will be used as an index.
- expires.conf: configures the expires, the cache_control and the etag directives. Defines map filters using content_type. MANDATORY.
- fastcgi.conf: configures common fastcgi settings.
- gzip.conf: configures gzip compression.
- headers.conf: adds few HTTP request and response headers customizations. MANDATORY.
- http2: configures http2.
- limits.conf: configures request processing rate.
- log.conf: defines log formats. MANDATORY.
- mime.conf: adds more mime types.
- nginx.conf: overrides the main nginx configuration.
- realip.conf: configures settings to get real_ip IP address in log files.
- ssl.conf: SSL configuration. MANDATORY.

### How to setup the NGINX personnal configuration

1. Copy the configuration [files](/src/conf-available) into /etc/nginx/conf-available
2. Edit the named like *.conf files and make changes as you need.
3. Enable the configuration:
  - using `./nginxenconf.sh <filename without extention>`. Ex: `./nginxenconf.sh headers`
  - or using `ln -s /etc/nginx/conf-available/headers.conf /etc/nginx/conf.d/headers.conf`
4. Test the configuration using `nginx -t`
5. When test is OK, activate the new configuration using `nginx -s reload` or `systemctl restart nginx.service`

## Templates

I wrote these templates to ease the process of creating server blocks.

Each domain.tld directory contains configuration for HTTP and HTTPS. The domain.tld/include contains the common snippets for HTTP and HTTPS.

The Content Security Policy (CSP) snippets depends on your site and must be tested.

### Features

- 000-default: contains the default Server Blocks configuration.
- static.tld: template for a static website.
- app.tld: template for a PHP application.
- api.tld: template for a mixed static website and PHP application.
- redirect.tld: template for a redirection.
- reverseproxy.tld: template for a reverse proxy.
- loader.conf: one file to rule them all.
- snippets: contains many files with common snippets.
  - **access_control directory** contains access control directives for application and static website.
  - **headers directory** contains CORS directives.
  - **security directory** contains security directives for access restriction, HSTS directives and WordPress security rules.

### How to setup the site templates

1. Copy the [templates](/src/sites-available) into /etc/nginx/sites-available
2. Edit the files and make changes as you need.
3. Edit and update the loader.conf file.
4. Enable the sites using `ln -s /etc/nginx/sites-available/loader.conf /etc/nginx/sites-enabled/loader`
5. Test the configuration using `nginx -t`
6. restarts the nginx daemon using `nginx -s reload`or `systemctl restart nginx.service`

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
