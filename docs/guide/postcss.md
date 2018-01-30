# PostCSS

Wee has departed from [Less](http://lesscss.org/), a traditional pre-processor, to [PostCSS](http://postcss.org/). This article will clarify what it is, why and how it is being used in Wee 4, and why it is worth knowing about.

At it's core, PostCSS is simply a tool for transforming CSS with JavaScript. If you are familiar with Less or Sass, you are familiar with the idea of pre-processors and how they define custom syntax to traditional CSS in order to allow for a more powerful set of tools and features for the developer that results in de-duplicated and elegant stylesheets. Using Sass or Less requires a build process for your front-end development that will transform the Sass/Less that you write into raw CSS. PostCSS is a peer in this respect. However, PostCSS is not just a pre-processor. Instead, it is a platform that provides the opportunity to custom tailor the way you compose and distribute CSS.

<img src="/uploads/general/postcss-anatomy.jpg" class="blog-image">

The diagram above shows the anatomy of PostCSS. At it's core, PostCSS is composed of a parser and a stringifier. The parser takes some text (CSS) and parses it out into an Abstract Syntax Tree (AST). Inversely, the stringifier takes the AST and turns it back into a string of text. What makes PostCSS special and what largely sets it apart from traditional pre-processors is the idea of plugins. PostCSS provides an API for registering plugins that allow for manipulating and working with the AST that was created by the parser. These plugins can do anything. There are plugins for writing Sass style variables, for auto-generating vendor prefixes to CSS declarations, for linting stylesheets, for minifying output, and the list goes on and on. With this ability to arrange plugins together gives near unlimited potential to what can be done for your composition of stylesheets. This is the potential we saw and why we took the leap to use PostCSS exclusively in Wee 4.

We have hopefully explained why we chose to use PostCSS, now let's look at how. Here are the plugins that are currently being used in the order they are being used in Wee:

- [postcss-variable-media](https://www.npmjs.com/package/postcss-variable-media)
- [autoprefixer](https://www.npmjs.com/package/autoprefixer)
- [cssnano](https://www.npmjs.com/package/cssnano)

## PostCSS Variable Media
This plugin allows for defining custom at-rules to represent media queries. It is crucial to the way that components are written in Wee 4 as it allows us to reference the same media queries across multiple component stylesheets. These references are then merged together in the final output CSS. In Wee 4, media queries are registered in the main configuration file `wee.json`. These are the default registered breakpoints:

```javascript
"breakpoints": {
	"mobileLandscape": 480,
	"tablet": 768,
	"desktop": 1024,
	"desktop2": 1280,
	"desktop3": 1440
}
```

The key of the object is the name of the breakpoint, and the number is assumed to be a min-width media query value in pixels. As an example of how these will be used, let's assume we have two different components. The styling below is assumed to be in two different component `index.pcss` files:

**Before**
```scss
// Component 1
@tablet {
    .component1 {
        background: #fff;
    }
}

// Component 2
@tablet {
    .component2 {
        font-size: 1.4rem;
    }
}
```

**After**
```css
@media (min-width: 768px) {
    .component1 {
        background: #fff;
    }
    .component2 {
        font-size: 1.4rem;
    }
}
```

In this way, we can separate and modularize our styling for an application (see guide for [Components](/guide/components)) while also being efficient with the number of media queries we are generating in our final CSS output.

### Autoprefixer
This is the defacto PostCSS plugin. If you don't already use it, you should start. In short, it adds vendor prefixes for CSS declarations automatically so you don't have to. Here is an example:

**Before**
```css
a {
    display: flex;
}
```

**After**
```css
a {
    display: -webkit-box;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex
}
```

## CSS Nano
This plugin minifies our final CSS output, hence it comes at the end of our plugin chain.
