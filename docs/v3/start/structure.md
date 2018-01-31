# Structure

Simple organization that's easy to navigate and extend

Wee begins with a Less stylesheet full of variables, a browser reset, a set of [mixins](/style/mixins) and [classes](/style/classes), and base styling. You also get example [HTML5](/start/markup), an [.htaccess](/start/structure#htaccess), sample favicons, [robots](/start/structure#robots)/[humans](/start/structure#humans).txt files, a robust [JavaScript library](/script/core), and a style guide template. Use it all or just parts, your choice

## browserconfig

Introduced in IE11, the [browserconfig](https://msdn.microsoft.com/en-us/library/dn320426(v=vs.85).aspx) file defines the icon configuration for Windows. By default the browser will look for the file in the root of the website.

```xml
<?xml version="1.0" encoding="utf-8"?><browserconfig><msapplication><tile><square70x70logosrc="/assets/img/icons/tile.png"/><square150x150logosrc="/assets/img/icons/tile.png"/><square310x310logosrc="/assets/img/icons/tile.png"/><wide310x150logosrc="/assets/img/icons/tile-wide.png"/><TileColor>#168eaf</TileColor></tile></msapplication></browserconfig>
```

## htaccess ##

Regardless if you’re running an xml-compatible web server the principles still apply. Avoid serving content from duplicate sources and present a consistent URL structure. Use this as a starting point.

### Maintenance

The maintenance block serves as a quick mechanism to toggle a temporary redirect to a maintenance page. It also has an IP exclusion to ensure that internal traffic can still access the full site.

```xml
RewriteCond %{REQUEST_URI} !^/maintenance\.html$
RewriteCond %{REMOTE_ADDR} !^123\.456\.789\.
RewriteCond $1 !^(assets) [NC]
RewriteRule ^(.*)$ /maintenance.html [R=307,L]
```

### Setup

A couple basic xml settings are made and the X-UA-Compatible header and encoding are set. If uncommented the two corresponding meta tags should be removed from the [HTML head](https://www.weepower.com/start/markup#meta).

```xml
RewriteEngine On
Options +FollowSymLinks -Indexes -MultiViews

# Internet Explorer document mode
Header set X-UA-Compatible "IE=edge"# Disable iframe embedding
Header always append X-Frame-Options SAMEORIGIN

# Character set
AddDefaultCharset utf-8
AddCharset utf-8 .atom .css .geojson .js .json .jsonld .manifest .map .rss .xml

# HTTP Strict Transport Security
Header always set Strict-Transport-Security "max-age=7776000; includeSubDomains"
```

### HTTP Access Control

[CORS headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS) open up web servers for cross-domain access. This is particularly helpful when serving assets through a pull CDN zone.

```xml
# Cross-origin images
<FilesMatch "\.(bmp|gif|ico|jpe?g|png|svg|webp)$">
    SetEnvIf Origin ":" IS_CORS
    Header set Access-Control-Allow-Origin "*" env=IS_CORS
</FilesMatch>

# Cross-origin web fonts
<FilesMatch "\.(eot|otf|ttf|woff2?)$">
    Header set Access-Control-Allow-Origin "*"
</FilesMatch>
```

### Errors

It’s important to intercept common HTTP errors on the host level with custom pages.

```xml
ErrorDocument 404 /404.html
```

### Project

Add your project’s specific rules to this section.

```xml
# Custom redirects and rewrites
```

### Rewrites

Without specific redirects most servers will allow multiple URLs to access the same endpoint. Funnel requests through redirect logic to ensure there is only one true canonical address.

```xml
# Force www
RewriteCond %{HTTP_HOST} !^www.weepower.com$ [NC]
RewriteRule ^(.*)$ http://www.weepower.com/$1 [R=301,L]# Remove www (use either force or remove)# RewriteCond %{HTTP_HOST} !^weepower.com$ [NC]# RewriteRule ^(.*)$ http://weepower.com/$1 [R=301,L]# Force SSL
RewriteCond %{HTTPS} !on
RewriteRule ^(.*)$ https://%{HTTP_HOST}/$1 [R=301,L]# Remove trailing slash
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)/$ /$1 [R=301,L]

# Remove multiple slashes
RewriteCond %{THE_REQUEST} //
RewriteRule ^(.*)$ /$1 [R=301,L]

# Remove index reference
RewriteCond %{REQUEST_URI} ^(.*/)index.html$ [NC]
RewriteRule . %1 [R=301,L]

# Remove extension
RewriteCond %{REQUEST_URI} ^GET\ (.*).html(.*)\ HTTP
RewriteRule (.*).html$ $1$2 [R=301]

# Rewrite extension
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME}.html -f
RewriteRule (.*) $1.html [L]
```

## humans

Of course you want robots to understand your site but what if humans take an interest? Use the `humans.txt` file to credit all your cool tools and languages.

## robots

Website owners use the `robots.txt` file to give instructions about their site to web robots, specifically what resources should be excluded from indexing.