# Markup

An example of responsible HTML development

## ARIA

[WAI-ARIA](http://www.w3.org/WAI/intro/aria) defines methods to ensure web content and applications are accessible to those with disabilities. It especially helps with dynamic content and JavaScript controls.

```html
<header role="banner"></header>
<nav role="navigation"><nav>
<main role="main"></main>
<footer role="contentinfo"></footer>
```

## Doctype

The doctype is a critical for communicating which standard to use when rendering your website. Wee uses HTML5, the modern, semantic format for structuring data which includes a number of new elements.

```html
<!doctype html>
```

## Icons

Whether someone is on a mobile device, legacy browser, or Windows tablet your brand should stay consistent. In addition to the iOS and Safari icons the `browserconfig.xml` and `favicon.ico` files serve most environments.

```html
<link rel="apple-touch-icon" href="/assets/img/icons/touch.png">
<link rel="mask-icon" href="/assets/img/icons/pin.svg" color="#349bb9">
```

To read more about the Safari 9 mask icon requirements check out the [Apple docs](https://developer.apple.com/library/prerelease/mac/releasenotes/General/WhatsNewInSafari/Articles/Safari_9.html).

## Legacy

Wee maintains compatibility with IE9 which requires [conditionally serving](http://www.quirksmode.org/css/condcom.html) specific rules and polyfills. If you aren’t supporting legacy browsers feel free to remove this.

```html
<!--[if lte IE 9]>
	<script src="/assets/js/ie9.min.js"></script>
<![endif]-->
```

## Meta

```html
<meta charset="utf-8">
<meta http-equiv="x-ua-compatible" content="ie=edge">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Front-End Framework | Wee</title>
<meta name="description" content="Blueprint for modern web development.">
```

It’s best to serve the meta charset and http-equiv values through HTTP headers. There are commented lines in the sample [.htaccess](/structure#htaccess) file for that purpose. If uncommented, you should remove the two tags from your HTML.

## Open Graph

The [Open Graph protocol](http://ogp.me/) enables any web page to become a rich object in a social graph. Both Facebook and Twitter leverage the tags for extracting page context when sharing.

```html
<meta property="og:type" content="website">
<meta property="og:site_name" content="Wee">
<meta property="og:title" content="Front-End Framework" itemprop="name">
<meta property="og:description" content="Blueprint for modern web development." itemprop="description">
<meta property="og:url" content="https://www.weepower.com" itemprop="url">
<meta property="og:image" content="https://www.weepower.com/assets/img/share.png" itemprop="image">
```

In the sample HTML Wee dual-purposes the Open Graph tags as [Schema properties](/docs/v3/start/markup?id=schema) for the WebPage scope defined on the document root.

## Publisher

While authorship is officially dead the publisher link is still being put to use according to Google.

```html
<link rel="publisher" href="https://plus.google.com/+weecss">
```

## Schema

[Schema](https://schema.org/) enables search engines to better understand the information on web pages and provide richer search results. It can also enable new tools and applications that make use of the tags.

```html
<html lang="en" itemscopeitemtype="http://schema.org/WebPage">
```

## Twitter Cards

With [Twitter Cards](https://dev.twitter.com/docs/cards), you can attach photos and other media to Tweets that drive traffic to your website.

Twitter cards can work in conjunction with Open Graph to eliminate duplicate tag content.