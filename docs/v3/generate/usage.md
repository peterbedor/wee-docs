# Usage

## Blocks

Blocks allow you to create and control modular sections of content

Within your templates you can create labelled blocks of content with the ability to output them. Content not in a block by default is pushed into the block labeled content.

### Tags

```
-~-blockName---

Lorem ipsum dolor

-~-blockName---

* Lorem
* Ipsum
* Dolor
```

```html
{{ #blocks }}
    {{ name }}
    {{ output|raw }}
{{ /blocks }}
```

### Appending & Rendering

By default blocks push into an iterable array of blocks given the same name. If you prefer to concatenate the content use the append filter. The render filter allows outputting the block inline as well as pushing it to the tag pair, useful when generating style guides.

-~-blockName|append|render---

### Custom Tags

You can create custom tags accessible in the blocks loop with the following format. Multiple tags are allowed.

-~-blockName|key:value|key2:value2---

Due to the parse order of the generator the examples above use leading `-~-` instead of the proper `---`.

## Content

With the content tag pair a section’s content can be looped through.

```html
{{ #content|tag }}
	<h1>{{ name }}</h1>
	<div>
		{{ output|raw }}
	</div>
{{ /content }}
```

### Input & Output

The input tag returns the raw markdown content before processing. The output tag returns the processed content.

```html
{{ #content }}
    {{ input }}
    {{ output }}
{{ /content }}
```

Since HTML entities are encoded by default the raw tag helper is needed to render markup.

## Data

The data tag is used to access any custom data inside of the data keys in the site file. This includes the site data, as well as data for individual sections. It can be used as a single tag or as a tag pair.

```
{{ data.version }}
{{ data.analyticsID }}
```

## Parent

The parent tag can be used to access the parent section of the current section.

```html
{{ #parent|notEmpty }}
	{{ parent.name }}
{{ /parent }}
```

## Sections

This is where you will specify the different sections of your site, and information related to each section. As the example below demonstrates, sections can be nested.

```
"sections": {
    "home": {
        "name": "Homepage",
        "data": {
            "seoTitle": "SEO Friendly Title",
        },
        "template": "index",
        "target": "public_html/index.html",
        "contentRoot": "home",
        "content": "body.md"
    },
    "blog": {
        "name": "Blog",
        "template": "blog",
        "target": [
            "public_html/blog/index.html"
        ],
        "content": "content/blog/*.md",
        "sections": {
            "entries": {
                "name": "Entries",
                "template": "entry",
                "target": [
                    "public_html/blog/.html"
                ],
                "content": "blog/*.md"
            }
        }
    }
}
```

### Name

The name for the section is set here and available to the template.

```
"name": "Section Name"
```

### Data

Any custom data that you may need for a section can be stored in the data object. They are accessible via `{{  }}` tags.

```
"data": {
    "sectionVariable": "value"
}
```

```
{{ data.sectionVariable }}
```

### Template

This is where you specify a section’s template. The html extension is assumed by default.

```
"template": "index"
```

### Target

This specifies the file to which the content will be written to.

```
"target": "public_html/index.html"
```

### Content

The files listed here contain the content that will be made available to the defined template. Files are compiled in the order that they are listed. A string or an array can be provided and all standard globbing patterns are supported.

```
"content": [
    "content/intro.md",
    "content/*.md"
]
```

## Site

The site tag enables access to any property specified at the root level of the site file.

### Name & Description

```html
<h1>{{ site.name }}</h1>
<span>{{ site.description }}</span>
```

### Sections

```html
<ul>
    {{ #site.sections }}
    <li>{{ name }}</li>
    {{ /site.sections }}
</ul>
```

### Environment

This will return the current development environment. Using this with the is filter, you can conditionally output content.

```
{{ #site.env|is(prod) }}
<script>// Script loaded only in production environment</script>
{{ /site.env }}
```

It also allows quick access to any data associated with an environment.

```html
<link rel="stylesheet" href="{{ site.assetUrl }}/style.css">
```

### Time

This will return the current time.

```
{{ site.time }}
```

## Target, Path & URL

Target tells you where the file is written in the file system. Path gives you the relative path. URL includes the domain.

```
{{ target }}
{{ path }}
{{ url }}
```