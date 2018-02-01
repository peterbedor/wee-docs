# Mixins

## Alignment

### Float

| Variable | Type   | Default | Description   | Required |
|----------|--------|---------|---------------|----------|
| @value   | preset | left    | Left or right | -        |
| @width   | unit   | -       | Width value   | -        |

```less|css
.float();

---


float: left;
```

```less|css
.float(right; 2);

---

float: right;
width: 2rem;
```

### Left & Right

```less|css
.left();
.right();

---

float: left;
float: right;
```

If a value is passed to the left or right mixins they reflect the left and right CSS properties and not float settings.

### Clearfix

```less|css
.clearfix();

---

&:after {
    clear: both;
    content: ' ';
    display: table;
}
```

### Clear

| Variable | Type   | Default | Description          | Required |
|----------|--------|---------|----------------------|----------|
| @value   | preset | both    | Both, left, or right | -        |

```less|css
.align(justify);
.align(middle);

---

text-align: justify;
vertical-align: middle;
```

### Vertical Align

| Variable | Type  | Default | Description     | Required |
|----------|-------|---------|-----------------|----------|
| @value   | value | -       | Alignment value | ✔        |

```less|css
.vertical-align(text-top);

---

vertical-align: text-top;
```

### Display

| Variable | Type  | Default | Description   | Required |
|----------|-------|---------|---------------|----------|
| @value   | value | -       | Display value | ✔        |

```less|css
.display(block);

---

display: block;
```

### Inline

```less|css
.inline();

---

display: inline;
```

### Inline-Block

| Variable | Type | Default | Description  | Required |
|----------|------|---------|--------------|----------|
| @width   | unit | -       | Width value  | -        |
| @height  | unit | -       | Height value | -        |

```less|css
.inline-block();

---

display: inline-block;
```

```less|css
.inline-block(4; 2);

---

display: inline-block;
width: 4rem;
height: 2rem;
```

## Animation

| Variable   | Type  | Default | Description     | Required |
|------------|-------|---------|-----------------|----------|
| @arguments | value | -       | Animation rules | ✔        |

```less|css
.animation(name 4s linear 0s1);

---

-webkit-animation: name 4slinear 0s 1;
animation: name 4slinear 0s 1;
```

### Keyframes

| Variable | Type  | Default | Description    | Required |
|----------|-------|---------|----------------|----------|
| @name    | value | -       | Animation name | ✔        |
| @start   | value | -       | Starting value | ✔        |
| @end     | value | -       | Ending value   | ✔        |

```less|css
.keyframes(fade-in, {
    .transparent();
}, {
    .opaque();
});

---

@-webkit-keyframes fade-in {
    0% {
        opacity: 0:
    }
    100% {
        opacity: 1:
    }
}
@keyframes fade-in {
    0% {
        opacity: 0:
    }
    100% {
        opacity: 1:
    }
}
```

## Backgrounds

| Variable | Type            | Default | Description      | Required |
|----------|-----------------|---------|------------------|----------|
| @value   | string, keyword | -       | Background rules | ✔        |

```less|css
.background(transparent);
.background('url("bg.png") #00f no-repeat');

---

background: transparent;
background: url("bg.png") #00fno-repeat;
```

| Variable  | Type            | Default                                                       | Description      | Required |
|-----------|-----------------|---------------------------------------------------------------|------------------|----------|
| @color    | color           | [@bodyBackground](/docs/v3/styles/variables?id=base) = @white | Background color | -        |
| @filename | string          | -                                                             | Image file       | -        |
| @repeat   | string, keyword | -                                                             | Image repeat     | -        |

| Variable | Type  | Default | Description        | Required |
|----------|-------|---------|--------------------|----------|
| @color   | color | -       | Background color   | ✔        |
| @opacity | unit  | -       | Background opacity | ✔        |

```less|css
.background(#00f; 0.2);

---

background-color: rgba(0, 0, 255, 0.2);
```

| Variable  | Type    | Default   | Description       | Required |
|-----------|---------|-----------|-------------------|----------|
| @color    | color   | -         | Background color  | ✔        |
| @filename | string  | -         | Image file        | ✔        |
| @x        | unit    | -         | Horizontal offset | ✔        |
| @y        | unit    | 0         | Vertical offset   | -        |
| @repeat   | keyword | no-repeat | Image repeat      | -        |

```less|css
.background(#00f; 'bg.png'; 10%; 15%);

---

background: #00furl('../img/bg.png') 10% 15% no-repeat;
```

| Variable  | Type   | Default                                                            | Description               | Required |
|-----------|--------|--------------------------------------------------------------------|---------------------------|----------|
| @value    | preset | -                                                                  | Light or dark             | ✔        |
| @opacity  | unit   | [@defaultOpacity](/docs/v3/styles/variables?id=miscellaneous) = .2 | Background                | -        |
| @fallback | color  | # fff, #000 #                                                      | Fallback background color | -        |

```less|css
.background(light; 50%);

---

background-color: rgba(255, 255, 255, 0.5);
```

### Background Color

| Variable | Type  | Default                                            | Description      | Required |
|----------|-------|----------------------------------------------------|------------------|----------|
| @color   | color | [base](/docs/v3/styles/variables?id=base) = @white | Background color | -        |

```less|css
.background-color(blue);

---

background-color: #00f;
```

### Background Image

| Variable | Type    | Default | Description | Required |
|----------|---------|---------|-------------|----------|
| @value   | keyword | -       | Image file  | ✔        |

```less|css
.background-image(bg.png);

---

background-image: '../img/bg.png';
```

| Variable  | Type    | Default | Description  | Required |
|-----------|---------|---------|--------------|----------|
| @filename | string  | -       | Image file   | ✔        |
| @repeat   | keyword | -       | Image repeat | -        |

```less|css
.background-image('bg.png'; no-repeat);

---

background-image: url('../img/bg.png');
background-repeat: no-repeat;
```

| Variable  | Type    | Default | Description   | Required |
|-----------|---------|---------|---------------|----------|
| retina    | keyword | -       | Retina preset | ✔        |
| @filename | string  | -       | Image file    | ✔        |
| @width    | unit    | auto    | Size or width | -        |
| @height   | unit    | auto    | Height        | -        |

```ccc|css
.selector {
    .background-image(retina; 'bg.png'; 10px);
}

---

.selector {
    background-image: url('../img/bg.png');
}
@media only screen and (-webkit-min-device-pixel-ratio: 1.3), (min--moz-device-pixel-ratio: 1.3), (min-resolution: 1.3dppx) {
    .selector {
        background-image: url('../img/bg-2x.png');
        background-size: 10px auto;
    }
}
```

| Variable  | Type    | Default   | Description       | Required |
|-----------|---------|-----------|-------------------|----------|
| @filename | string  | -         | Image file        | ✔        |
| @x        | unit    | -         | Horizontal offset | ✔        |
| @y        | unit    | 0         | Vertical offset   | -        |
| @repeat   | keyword | no-repeat | Repeat            | -        |

```ccc|css
.background-image('bg.png'; 10px);

---

background-image: url('../img/bg.png');
background-position: 10px 0;
background-repeat: no-repeat;
```

| Variable  | Type    | Default   | Description     | Required |
|-----------|---------|-----------|-----------------|----------|
| retina    | keyword | -         | Retina present  | ✔        |
| @filename | string  | -         | Image file      | ✔        |
| @width    | unit    | -         | Width           | ✔        |
| height    | unit    | -         | Height          | ✔        |
| @x        | unit    | 0         | Vertical offset | -        |
| @repeat   | keyword | no-repeat | Image repeat    | -        |

```ccc|css
.selector {
    .background-image(retina; 'bg.png'; 4rem; 3rem; 10px);
}

---

.selector {
    background-image: url('../img/bg.png');
    background-position: 10px0;
    background-repeat: no-repeat;
}
@media only screen and (-webkit-min-device-pixel-ratio: 1.3), (min--moz-device-pixel-ratio: 1.3), (min-resolution: 1.3dppx) {
    .selector {
        background-image: url('../img/bg-2x.png');
        background-size: 4rem3rem;
    }
}
```

The value of the retina filename suffix is set by the `@retinaSuffix`[variable](/docs/v3/styles/variables?id=images).

| Variable    | Type    | Default   | Description       | Required |
|-------------|---------|-----------|-------------------|----------|
| @filename   | string  | -         | Image file        | ✔        |
| @x          | unit    | -         | Horizontal offset | ✔        |
| @y          | unit    | 0         | Vertical offset   | ✔        |
| @repeat     | keyword | no-repeat | Image repeat      | ✔        |
| @attachment | keyword | -         | Image attachment  | ✔        |

```ccc|css
.background-image('bg.png'; 10px; 8px; no-repeat; fixed);

---

background-attachment: fixed;
background-image: url('../img/bg.png');
background-position: 10px 8px;
background-repeat: no-repeat;
```

| Variable    | Type    | Default | Description       | Required |
|-------------|---------|---------|-------------------|----------|
| retina      | preset  | -       | Retina            | ✔        |
| @filename   | string  | -       | Image file        | ✔        |
| @width      | unit    | -       | Width value       | ✔        |
| height      | unit    | -       | Height value      | ✔        |
| @x          | unit    | -       | Horizontal offset | ✔        |
| @y          | unit    | -       | Vertical offset   | ✔        |
| @repeat     | keyword | -       | Image repeat      | ✔        |
| @attachment | keyword | -       | Attachment value  | ✔        |

```ccc|css
.selector {
    .background-image(retina; 'bg.png'; 4rem; 3rem; 10px; 8px; no-repeat; fixed);
}

---

.selector {
    background-attachment: fixed;
    background-image: url('../img/bg.png');
    background-position: 10px8px;
    background-repeat: no-repeat;
}
@media only screen and (-webkit-min-device-pixel-ratio: 1.3), (min--moz-device-pixel-ratio: 1.3), (min-resolution: 1.3dppx) {
    .selector {
        background-image: url('../img/bg-2x.png');
        background-size: 4rem3rem;
    }
}
```

| Variable    | Type    | Default | Description       | Required |
|-------------|---------|---------|-------------------|----------|
| @filename   | string  | -       | Image file        | ✔        |
| @x          | unit    | -       | Horizontal offset | ✔        |
| @y          | unit    | -       | Vertical offset   | ✔        |
| @repeat     | keyword | -       | Repeat            | ✔        |
| @attachment | keyword | -       | Attachment value  | ✔        |
| @size       | unit    | -       | Size              | ✔        |

```ccc|css
.background-image('bg.png'; 10px; 8px; no-repeat; fixed; 40);

---

background-attachment: fixed;
background-image: url('../img/bg.png');
background-position: 10px 8px;
background-repeat: no-repeat;
background-size: 40rem;
```

| Variable    | Type    | Default | Description       | Required |
|-------------|---------|---------|-------------------|----------|
| @filename   | string  | -       | Image file        | ✔        |
| @x          | unit    | -       | Horizontal offset | ✔        |
| @y          | unit    | -       | Vertical offset   | ✔        |
| @repeat     | keyword | -       | Repeat            | ✔        |
| @attachment | keyword | -       | Attachment value  | ✔        |
| @width      | unit    | -       | Width             | ✔        |
| @height     | unit    | -       | Height            | ✔        |

```ccc|css
.background-image('bg.png'; 10px; 8px; no-repeat; fixed; 400px; 300px);

---

background-attachment: fixed;
background-image: url('../img/bg.png');
background-position: 10px 8px;
background-repeat: no-repeat;
background-size: 400px 300px;
```

### Background Gradient ### (.doc__label .doc__variables__label)

| Variable | Type    | Default                                         | Description    | Required |
|----------|---------|-------------------------------------------------|----------------|----------|
| @color   | color   | [@gray](/docs/v3/styles/variables?id=grayscale) | Fallback color | -        |
| @start   | color   | rgba(0,0,0,0.8)                                 | Starting color | -        |
| @end     | color   | rgba(0,0,0,0.2)                                 | Ending color   | -        |
| @angle   | integer | 180                                             | Angle          | -        |

```ccc|css
.background-gradient(blue; green; yellow; 90);

---

background-color: #00f;
background: -webkit-linear-gradient(0deg, #008000, #ff0);
background: linear-gradient(90deg, #008000, #ff0);
```

| Variable | Type       | Default | Description    | Required |
|----------|------------|---------|----------------|----------|
| @color   | color      | @gray   | Fallback color | -        |
| @spread  | percentage | -       | Color range    | ✔        |
| @angle   | integer    | 180     | Angle          | -        |

```ccc|css
.background-gradient(blue; 15%; 90);

---

background-color: #00f;
background: -webkit-linear-gradient(0deg, #4d4dff, #0000b3);
background: linear-gradient(90deg, #4d4dff, #0000b3);
filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#4d4dff', endColorstr='#0000b3', GradientType=0);
```

### Background Attachment

| Variable   | Type    | Default | Description      | Required |
|------------|---------|---------|------------------|----------|
| @arguments | keyword | -       | Attachment value | ✔        |

```ccc|css
.background-attachment(scroll);

---

background-attachment: scroll;
```

### Background Position

| Variable | Type | Default | Description       | Required |
|----------|------|---------|-------------------|----------|
| @x       | unit | 0       | Horizontal offset | -        |
| @y       | unit | 0       | Vertical offset   | -        |

```ccc|css
.background-position(10px; 5px);

---

background-position: 10px 5px;
```

### Background Repeat

| Variable   | Type    | Default | Description  | Required |
|------------|---------|---------|--------------|----------|
| @arguments | keyword | -       | Repeat value | ✔        |

```ccc|css
.background-repeat(repeat);

---

background-repeat: repeat;
```

### Background Size

| Variable | Type | Default | Description | Required |
|----------|------|---------|-------------|----------|
| @size    | unit | -       | Size value  | ✔        |

```ccc|css
.background-size(3rem);

---

background-size: 3rem;
```

### Background Clip

| Variable | Type    | Default    | Description | Required |
|----------|---------|------------|-------------|----------|
| @value   | keyword | border-box | Clip value  | -        |

```ccc|css
.background-clip();

---

background-clip: border-box;
```

### Sprite

| Variable  | Type    | Default         | Description       | Required |
|-----------|---------|-----------------|-------------------|----------|
| @color    | color   | -               | Background color  | ✔        |
| @x        | unit    | 0               | Horizontal offset | -        |
| @y        | unit    | 0               | Vertical offset   | -        |
| @repeat   | keyword | no-repeat       | Repeat            | -        |
| @filename | string  | @spriteFilename | Image file        | -        |

```ccc|css
.sprite(blue);

---

background: #00furl('../img/sprite.png') 0 0 no-repeat;
```

| Variable  | Type    | Default         | Description       | Required |
|-----------|---------|-----------------|-------------------|----------|
| retina    | keyword | -               | Retina preset     | ✔        |
| @color    | color   | -               | Background Color  | ✔        |
| @width    | unit    | auto            | Width             | -        |
| @height   | unit    | auto            | Height            | -        |
| @x        | unit    | 0               | Horizontal offset | -        |
| @y        | unit    | 0               | Vertical offset   | -        |
| @repeat   | keyword | no-repeat       | Repeat            | -        |
| @filename | string  | @spriteFilename | Image file        | -        |

```ccc|css
.selector {
    .sprite(retina; blue);
}

---

.selector {
    background: #0000ffurl('../img/sprite.png') 00 no-repeat;
}
@media only screen and (-webkit-min-device-pixel-ratio: 1.3), (min--moz-device-pixel-ratio: 1.3), (min-resolution: 1.3dppx) {
    .selector {
        background-image: url('../img/sprite-2x.png');
        background-size: auto auto;
    }
}
```

| Variable  | Type    | Default         | Description       | Required |
|-----------|---------|-----------------|-------------------|----------|
| @x        | unit    | 0               | Horizontal offset | -        |
| @y        | unit    | -0              | Vertical offset   | -        |
| @repeat   | keyword | no-repeat       | Repeat            | -        |
| @filename | string  | @spriteFilename | Image file        | -        |

```less|css
.sprite();

---

background-image: url('../img/sprite.png');
background-position: 0 0;
background-repeat: no-repeat;
```

| Variable  | Type    | Default             | Description       | Required |
|-----------|---------|---------------------|-------------------|----------|
| retina    | keyword | -                   | Retina preset     | ✔        |
| @x        | unit    | 0                   | Horizontal offset | -        |
| @y        | unit    | 0                   | Vertical offset   | -        |
| @width    | unit    | @retinaSpriteWidth  | Width             | -        |
| @height   | unit    | @retinaSpriteHeight | Height            | -        |
| @repeat   | keyword | no-repeat           | Repeat            | -        |
| @filename | string  | @spriteFilename     | Image file        | -        |

```
.selector {
    .sprite(retina);
}

---

.selector {
    background-image: url('../img/sprite.png');
    background-position: 00;
    background-repeat: no-repeat;
}
@media only screen and (-webkit-min-device-pixel-ratio: 1.3), (min--moz-device-pixel-ratio: 1.3), (min-resolution: 1.3dppx) {
    .selector {
        background-image: url('../img/sprite-2x.png');
        background-size: auto auto;
    }
}
```

All image paths are relative to the @imagePath variable which defaults to "…/img". It can be overridden in variables.less.

## Blocks

### Centered Block

| Variable  | Type | Default | Description   | Required |
|-----------|------|---------|---------------|----------|
| @maxWidth | unit | -       | Max width     | -        |
| @margin   | unit | -       | Bottom margin | -        |

```less|css
.centered-block();

---

display: block;
margin-left: auto;
margin-right: auto;
```

```less|css
.centered-block(5);

---

display: block;
margin-left: auto;
margin-right: auto;
max-width: 5rem;
```

```less|css
.centered-block(50%; 2);

---

display: block;
margin-left: auto;
margin-right: auto;
max-width: 50%;
margin-bottom: 2rem;
```

## Borders

### Border

| Variable | Type            | Default             | Description  | Required |
|----------|-----------------|---------------------|--------------|----------|
| @value   | string, keyword | '1px solid #404040' | Border rules | ✔        |

```less|css
.border('2px dotted #00f');

---

border: 2pxdotted#00f;
```

| Variable | Type    | Default      | Description | Required |
|----------|---------|--------------|-------------|----------|
| @color   | color   | @lighterGray | Color       | -        |
| @value   | unit    | 1px          | Size        | -        |
| @style   | keyword | solid        | Style       | -        |

```less|css
.border(red; 4px; dotted);

---

border: 4pxdotted#f00;
```

| Variable    | Type    | Default              | Description          | Required |
|-------------|---------|----------------------|----------------------|----------|
| light, dark | keyword | -                    | Light or dark preset | ✔        |
| @opacity    | integer | @defaultOpacity = .2 | Opacity              | -        |
| @value      | unit    | 1px                  | Width                | -        |
| @style      | keyword | solid                | Border style         | -        |
| @fallback   | color   | @black = #000        | Fallback color       | -        |

```less|css
.border(dark; 40%; 2px);

---

border: 2px solid rgba(0, 0, 0, 0.4);
```

| Variable                 | Type    | Default                     | Description | Required |
|--------------------------|---------|-----------------------------|-------------|----------|
| top, right, bottom, left | keyword | -                           | Side preset | ✔        |
| @color                   | color   | @lighterGray = @darkestGray | Color       | -        |
| @value                   | unit    | 1px                         | Width       | -        |
| @style                   | keyword | solid                       | Style       | -        |

```less|css
.border(top; blue);

---

border-top: 1pxsolid#00f;
```

| Variable                 | Type    | Default                      | Description          | Required |
|--------------------------|---------|------------------------------|----------------------|----------|
| top, right, bottom, left | keyword | -                            | Side preset          | ✔        |
| light, dark              | keyword | -                            | Light or dark preset | ✔        |
| @opacity                 | integer | @defaultOpacity = .2         | Color                | -        |
| @value                   | unit    | 1px                          | Width                | -        |
| @style                   | keyword | solid                        | Style                | -        |
| @fallback                | color   | @white = #fff, @black = #000 | Fallback color       | -        |

```less|css
.border(top; light; 50%; 3px; dotted);

---

border: 3pxdottedrgba(255, 255, 255, 0.5);
```

| Variable             | Type    | Default                     | Description                   | Required |
|----------------------|---------|-----------------------------|-------------------------------|----------|
| horizontal, vertical | keyword | -                           | Horizontal or vertical preset | ✔        |
| @color               | color   | @lighterGray = @darkestGray | Color                         | -        |
| @value               | unit    | 1px                         | Width                         | -        |
| @style               | keyword | solid                       | Style                         | -        |

```less|css
.border(horizontal; red; 2px; dotted);

---

border-left: 2pxdotted#ff0000;
border-right: 2pxdotted#ff0000;
```

| Variable             | Type    | Default              | Description                   | Required |
|----------------------|---------|----------------------|-------------------------------|----------|
| horizontal, vertical | keyword | -                    | Horizontal or vertical preset | ✔        |
| light, dark          | keyword | -                    | Light or dark preset          | ✔        |
| @opacity             | integer | @defaultOpacity = .2 | Opacity                       | -        |
| @value               | unit    | 1px                  | Width                         | -        |
| @style               | keyword | solid                | Style                         | -        |

```less|css
.border(vertical; dark; 0.4);

---

border-top: 1pxsolidrgba(0, 0, 0, 0.4);
border-bottom: 1pxsolidrgba(0, 0, 0, 0.4);
```

| Variable | Type    | Default                     | Description | Required |
|----------|---------|-----------------------------|-------------|----------|
| @top     | unit    | -                           | Top size    | ✔        |
| @right   | unit    | -                           | Right size  | -        |
| @bottom  | unit    | -                           | Bottom size | -        |
| @left    | unit    | -                           | Left size   | -        |
| @color   | color   | @lighterGray = @darkestGray | Color       | -        |
| @style   | keyword | solid                       | Style       | -        |

```less|css
.border(1px; 3px; 4px; 2px; blue; dotted);

---

border-bottom: 4pxdotted#00f;
border-left: 2pxdotted#00f;
border-right: 3pxdotted#00f;
border-top: 1pxdotted#00f;
```

### Border Image

| Variable  | Type    | Default | Description              | Required |
|-----------|---------|---------|--------------------------|----------|
| @filename | string  | -       | Name of file             | -        |
| @slice    | unit    | 100%    | Slice offset             | -        |
| @width    | unit    | 1       | Border width             | -        |
| @outset   | unit    | 0       | Extend beyond border box | -        |
| @repeat   | keyword | stretch | Match size of border     | -        |

```less|css
.border-image('border.png');

---

-webkit-border-image: url('../img/border.png') 100% 1 0 stretch;
border-image: url('../img/border.png') 100% 1 0 stretch;
```

### Border Color, Style & Width

| Variable               | Type                 | Default | Description            | Required |
|------------------------|----------------------|---------|------------------------|----------|
| @color, @style, @width | color, keyword, unit | -       | Color, style, or width | ✔        |

```less|css
.border-color(blue);

---

border-color: #00f;
```

| Variable                 | Type                 | Default | Description            | Required |
|--------------------------|----------------------|---------|------------------------|----------|
| top, right, bottom, left | keyword              | -       | Side presets           | ✔        |
| @color, @style, @width   | color, keyword, unit | -       | Color, style, or width | ✔        |

```less|css
.border-color(top; blue);

---

border-top-color: #00f;
```

```less|css
.border-style(dotted);

---

border-style: dotted;
```

```less|css
.border-style(right; dotted);

---

border-right-style: dotted;
```

```less|css
.border-width(4px);

---

border-width: 4px;
```

```less|css
.border-width(bottom; 4px);

---

border-bottom-width: 4px;
```

## Box Shadows

| Variable | Type            | Default                                        | Description      | Required |
|----------|-----------------|------------------------------------------------|------------------|----------|
| @value   | string, keyword | '1px 1px 0 0 rgba(0, 0, 0, @{defaultOpacity})' | Box-shadow rules | -        |

```less|css
.shadow('3px 2px 1px 0 #000');

---

box-shadow: 3px2px1px0#000;
```

| Variable | Type    | Default | Description       | Required |
|----------|---------|---------|-------------------|----------|
| inner    | keyword | -       | Inner preset      | -        |
| @color   | color   | -       | Shadow color      | ✔        |
| @x       | value   | 1px     | Horizontal offset | -        |
| @y       | value   | 1px     | Vertical offset   | -        |
| @blur    | value   | 0       | Blur distance     | -        |
| @spread  | value   | 0       | Shadow size       | -        |

```less|css
.shadow(blue);

---

box-shadow: 1px 1px 0 0 #00f;
```

```less|css
.shadow(rgba(0, 0, 0, 0.6); 4px; 3px; 2px; 2px);

---

box-shadow: 4px 3px 2px 2pxrgba(0, 0, 0, 0.6);
```

```less|css
.shadow(inner; blue);

---

box-shadow: inset 1px 1px 0 0 #00f;
```

| Variable    | Type        | Default              | Description          | Required |
|-------------|-------------|----------------------|----------------------|----------|
| light, dark | keyword     | -                    | Light or dark preset | ✔        |
| @value      | @percentage | @defaultOpacity = .2 | Opacity              | -        |
| @x          | unit        | 1px                  | Horizontal offset    | -        |
| @y          | unit        | 1px                  | Vertical offset      | -        |
| @blur       | unit        | 0                    | Blur                 | -        |
| @spread     | unit        | 0                    | Spread               | -        |

```less|css
.shadow(light; 40%);

---

box-shadow: 1px 1px 0 0 rgba(255, 255, 255, 0.4);
```

```less|css
.shadow(dark; 50%);

---

box-shadow: 1px 1px 0 0 rgba(0, 0, 0, 0.5);
```

| Variable    | Type       | Default              | Description          | Required |
|-------------|------------|----------------------|----------------------|----------|
| inner       | keyword    | -                    | Inner preset         | ✔        |
| light, dark | keyword    | -                    | Light or dark preset | ✔        |
| @opacity    | percentage | @defaultOpacity = .2 | Opacity              | -        |
| @x          | unit       | 1px                  | Horizontal offset    | -        |
| @y          | unit       | 1px                  | Vertical offset      | -        |
| @blur       | unit       | 0                    | Blur                 | -        |
| @spread     | unit       | 0                    | Spread               | -        |

```less|css
.shadow(inner; light; 40%);

---

box-shadow: inset 1px 1px 0 0 rgba(255, 255, 255, 0.4);
```

```less|css
.shadow(inner; dark; 50%);

---

box-shadow: inset 1px 1px 0 0 rgba(0, 0, 0, 0.5);
```

## circle

```css
circle(diameter, crop, display = 'block')
```

```less|css
.circle(.5);

---

height: 0.5rem;
width: 0.5rem;
display: block;
background-clip: border-box;
border-radius: 0.25rem;
```

```less|css
.circle(.5, true);

---

height: 0.5rem;
width: 0.5rem;
display: block;
background-clip: border-box;
border-radius: 0.25rem;
overflow: hidden;
```

```less|css
.circle(.5, display: inline);

---

height: 0.5rem;
width: 0.5rem;
display: inline-block;
background-clip: border-box;
border-radius: 0.25rem;
```

## clearfix

```less|css
.clearfix();

---

&:after {
    clear: both;
    content: '';
    display: block;
}
```

##

| Variable | Type  | Default                   | Description | Required |
|----------|-------|---------------------------|-------------|----------|
| @color   | color | @baseColor = @darkestGray | Color value | -        |

```less|css
.color(blue);

---

color: #00f;
```

### Shortcuts

```css
.primary();
.secondary();
.tertiary();
.white();
.lightestGray();
.lighterGray();
.lightGray();
.gray();
.darkGray();
.darkerGray();
.darkestGray();
.black();
```

The values for all the above colors are configurable with [variables.less](/style/variables).

## Content

| Variable | Type            | Default | Description | Required |
|----------|-----------------|---------|-------------|----------|
| @value   | string, keyword | ''      | Content     | -        |
| @font    | string, keyword | false   | Font family | -        |
| @size    | unit            | false   | Font size   | -        |

```less|css
.content(text);

---

content: 'text';
```

```less|css
.content(example; Georgia; 2);

---

content: 'example';
font-family: Georgia;
font-size: 2rem;
```

### Prefix, Suffix & Bookends

| Variable | Type            | Default | Description          | Required |
|----------|-----------------|---------|----------------------|----------|
| @value   | string, keyword | '-'     | Content              | -        |
| @margin  | unit            | 0.5em   | Left or right margin | -        |
| @font    | string, keyword | false   | Font family          | -        |
| @color   | color           | false   | Font color           | -        |

```less|css
.prefix();

---

:before {
    content: '-';
    margin-right: 0.5em;
}
```

```less|css
.suffix('text'; 1em; Georgia; blue);

---

:after {
    content: 'text';
    margin-left: 1em;
    font-family: Georgia;
    color: #0000ff;
}
```

```less|css
.bookends();

---

:before {
    content: '-';
    margin-right: 0.5em;
}
:after {
    content: '-';
    margin-left: 0.5em;
}
```

## Display

### Hide

```less|css
.hide();

---

display: none;
```

### Show

```less|css
.show();

---

display: inherit;
```

### Hidden

```less|css
.hidden();

---

visibility: hidden;
```

### Visible

```less|css
.visible();

---

visibility: visible;
```

### Block

| Variable | Type | Default | Description | Required |
|----------|------|---------|-------------|----------|
| @width   | unit | -       | Width       | ✔        |
| @height  | unit | -       | Height      | -        |

```less|css
.block(4; 3);

---

display: block;
width: 4rem;
height: 3rem;
```

### Spaced

| Variable | Type | Default                | Description   | Required |
|----------|------|------------------------|---------------|----------|
| @margin  | unit | @blockMarginBottom = 4 | Bottom margin | -        |

```less|css
.spaced(0.5);

---

margin-bottom: 0.5rem;
```

### Spaced Block

| Variable | Type | Default                | Description   | Required |
|----------|------|------------------------|---------------|----------|
| @margin  | unit | @blockMarginBottom = 4 | Bottom margin | -        |
| @width   | unit | -                      | Width         | -        |
| @height  | unit | -                      | Height        | -        |

```less|css
.spaced-block(0.5; 2; 4);

---

display: block;
margin-bottom: 0.5rem;
width: 2rem;
height: 4rem;
```

### Box Sizing

| Variable | Type    | Default    | Description      | Required |
|----------|---------|------------|------------------|----------|
| @val     | keyword | border-box | Box-sizing value | -        |

```less|css
.box-sizing(content-box);

---

-moz-box-sizing: content-box;
-webkit-box-sizing: content-box;
box-sizing: content-box;
```

### Border Box

```less|css
.border-box();

---

-moz-box-sizing: border-box;
-webkit-box-sizing: border-box;
box-sizing: border-box;
```

### Content Box

```less|css
.content-box();

---

-moz-box-sizing: content-box;
-webkit-box-sizing: content-box;
box-sizing: content-box;
```

## fill

```less|css
.fill();

---

height: 100%;
width: 100%;
```

## Filters

### Filter

| Variable | Type            | Default | Description  | Required |
|----------|-----------------|---------|--------------|----------|
| @value   | string, keyword | -       | Filter rules | ✔        |

```less|css
.filter('grayscale(50%)');

---

-webkit-filter: grayscale(50%);
filter: grayscale(50%);
```

### Blur ### (.doc__label .doc__variables__label)

| Variable | Type | Default | Description | Required |
|----------|------|---------|-------------|----------|
| @value   | unit | 2px     | Radius      | -        |

```less|css
.blur(4px);

---

-webkit-filter: blur(4px);
filter: blur(4px);
```

### Brightness

| Variable | Type | Default | Description | Required |
|----------|------|---------|-------------|----------|
| @value   | unit | 0.5     | Multiplier  | -        |

```less|css
.brightness(0.8);

---

-webkit-filter: brightness(0.8);
filter: brightness(0.8);
```

### Contrast

| Variable | Type | Default | Description | Required |
|----------|------|---------|-------------|----------|
| @value   | unit | 1.5     | Multiplier  | -        |

```less|css
.contrast(1.2);

---

-webkit-filter: contrast(1.2);
filter: contrast(1.2);
```

### Grayscale

| Variable | Type | Default | Description | Required |
|----------|------|---------|-------------|----------|
| @value   | unit | 1       | Amount      | -        |

```less|css
.grayscale();

---

-webkit-filter: grayscale(1);
filter: grayscale(1);
```

### Hue Rotate

| Variable | Type | Default | Description | Required |
|----------|------|---------|-------------|----------|
| @value   | unit | 180deg  | Angle       | -        |

```less|css
.hue-rotate(60deg);

---

-webkit-filter: hue-rotate(60deg);
filter: hue-rotate(60deg);
```

### Invert

| Variable | Type | Default | Description | Required |
|----------|------|---------|-------------|----------|
| @value   | unit | 1       | Amount      | -        |

```less|css
.invert(20%);

---

-webkit-filter: invert(20%);
filter: invert(20%);
```

### Saturate

| Variable | Type | Default | Description | Required |
|----------|------|---------|-------------|----------|
| @value   | unit | 0.5     | Amount      | -        |

```less|css
.saturate(200%);

---

-webkit-filter: saturate(200%);
filter: saturate(200%);
```

### Sepia

| Variable | Type | Default | Description | Required |
|----------|------|---------|-------------|----------|
| @value   | unit | 0.5     | Amount      | -        |

```less|css
.sepia(100%);

---

-webkit-filter: sepia(100%);
filter: sepia(100%);
```

### Drop Shadow

| Variable | Type            | Default                                      | Description       | Required |
|----------|-----------------|----------------------------------------------|-------------------|----------|
| @value   | string, keyword | '1px 1px 0 rgba(0, 0, 0, @{defaultOpacity})' | Drop-shadow rules | -        |

```less|css
.drop-shadow('2px 2px 1px rgba(120, 80, 40, 0.5)');

---

filter: drop-shadow('2px 2px 1pxrgba(120, 80, 40, 0.5)');
```

| Variable | Type  | Default | Description | Required |
|----------|-------|---------|-------------|----------|
| @color   | color | -       | Color       | ✔        |
| @x       | unit  | 1px     | X-offset    | -        |
| @y       | unit  | 1px     | Y-offset    | -        |
| @blur    | unit  | 0       | Blur radius | -        |

```less|css
.drop-shadow(blue; 2px; 4px; 1px);

---
```css
filter: drop-shadow('2px 4px 1px#00f');
```

```less|css
.drop-shadow(light; 0.4);

---

filter: drop-shadow('1px 1px 0 rgba(255, 255, 255, 0.4)');
```

```less|css
.drop-shadow(dark; 0.8; 2px; 1px; 1px);

---

filter: drop-shadow('2px 1px 1pxrgba(0, 0, 0, 0.8)');
```

## Font Family ## (#font-family .doc__title)

| Variable | Type            | Default                                  | Description       | Required |
|----------|-----------------|------------------------------------------|-------------------|----------|
| @value   | string, keyword | @baseFont = Arial, Helvetica, sans-serif | Font family rules | -        |

```less|css
.font-family(Georgia, Serif);

---

font-family: Georgia, Serif;
```

## Font Loading

### Load Font

| Variable | Type             | Default | Description       | Required |
|----------|------------------|---------|-------------------|----------|
| @name    | string           | -       | Font family rules | ✔        |
| @file    | file             | @name   | Font file         | -        |
| @weight  | integer, keyword | normal  | Font weight       | -        |
| @style   | keyword          | normal  | Font style        | -        |

```less|css
.load-font(icons);

---

@font-face {
    font-family: Example;
        src: url('../fonts/icons.eot');
        src: url('../fonts/icons.eot?#iefix') format('embedded-opentype'),
            url('../fonts/icons.woff2') format('woff2'),
             url('../fonts/icons.woff') format('woff'),
             url('../fonts/icons.ttf') format('truetype');
        font-style: normal;
        font-weight: normal;

    // Window Chrome fix
    @media screen and (-webkit-min-device-pixel-ratio: 0) {
        @font-face {
            font-family: ~'@{name}';
            src: url('../fonts/icons.svg#icons') format('svg');
        }
    }
}
```

## Font Selection

| Variable    | Type    | Default                                  | Description       | Required |
|-------------|---------|------------------------------------------|-------------------|----------|
| @family     | font    | @baseFont = Arial, Helvetica, sans-serif | Font family rules | -        |
| @size       | unit    | -                                        | Font size         | -        |
| @weight     | unit    | -                                        | Font weight       | -        |
| @lineHeight | unit    | -                                        | Line height       | -        |
| @style      | keyword | -                                        | Font style        | -        |

```less|css
.font(Helvetica; 2; 100; 2; italic);

---

font-family: Helvetica;
font-size: 2rem;
font-weight: 100;
line-height: 2rem;
font-style: italic;
```

## Font Size

| Variable | Type | Default             | Description | Required |
|----------|------|---------------------|-------------|----------|
| @value   | unit | @baseFontSize = 1.6 | Font size   | -        |

```less|css
.font-size(2);

---

font-size: 2rem;
```

| Variable    | Type | Default | Description       | Required |
|-------------|------|---------|-------------------|----------|
| @value      | unit | -       | Font size rules   | ✔        |
| @lineHeight | unit | -       | Line height rules | ✔        |

```less|css
.font-size(3; 1.6);

---

font-size: 3rem;
line-height: 1.6rem;
```

## Font Style

| Variable | Type    | Default | Description | Required |
|----------|---------|---------|-------------|----------|
| @value   | keyword | normal  | Font style  | -        |

```less|css
.font-style(italic);

---

font-style: italic;
```

## Font Weight

| Variable | Type | Default                  | Description | Required |
|----------|------|--------------------------|-------------|----------|
| @value   | unit | @baseFontWeight = normal | Font weight | -        |

```less|css
.font-weight(300);

---

font-weight: 300;
```

## Forms

### Input Placeholder

| Variable | Type  | Default                                            | Description       | Required |
|----------|-------|----------------------------------------------------|-------------------|----------|
| @color   | color | @inputPlaceholderColor = lighten(@inputColor, 40%) | Placeholder color | -        |

```less|css
.input-placeholder(gray);

---

:-moz-placeholder {
    color: #808080;
}
::-moz-placeholder {
    color: #808080;
}
:-ms-input-placeholder {
    color: #808080;
}
::-webkit-input-placeholder {
    color: #808080;
}
```

## Grid

### Row & Row-Modify

| Variable | Type       | Default          | Description | Required |
|----------|------------|------------------|-------------|----------|
| @margin  | percentage | @gridMargin = 5% | Left margin | -        |

```less|css
.selector {
    .row(2%);
}

---

.selector {
    margin-left: -2%;
    max-width: 102%;
}
.selector:after {
    clear: both;
    content: ' ';
    display: table;
}
```

```less|css
.row-modify(2%);

---

margin-left: -2%;
max-width: 102%;
```

### Row Reset

```less|css
.row-reset();

---

margin-left: 0;
max-width: none;
```

### Column & Column-Modify

| Variable | Type | Default | Description  | Required |
|----------|------|---------|--------------|----------|
| @width   | unit | false   | Column width | -        |

```less|css
.column(30%);

---

float: left;
width: 30%;
```

| Variable | Type       | Default          | Description                | Required |
|----------|------------|------------------|----------------------------|----------|
| spaced   | keyword    | -                | Set margin between columns | -        |
| @share   | integer    | -                | Column span                | ✔        |
| @columns | integer    | @gridColumns = 8 | Number of columns          | -        |
| @margin  | percentage | @gridMargin = 5% | Left margin                | -        |

```less|css
.column(2; 3);

---

float: left;
width: 66.66666667%;
```

```less|css
.column(spaced; 2; 3; 2%);

---

float: left;
width: 64.66666667%;
margin-left: 2%;
```

```less|css
.column-modify(spaced; 2; 3; 2%);

---

width: 64.66666667%;
margin-left: 2%;
```

### Column Reset

| Variable     | Type    | Default | Description       | Required |
|--------------|---------|---------|-------------------|----------|
| @resetMargin | boolean | false   | Reset left margin | -        |

```less|css
.column-reset(true);

---

float: none;
width: auto;
margin-left: 0;
```

### Column Pull & Push

| Variable | Type    | Default          | Description       | Required |
|----------|---------|------------------|-------------------|----------|
| @share   | integer | -                | Column span       | ✔        |
| @columns | integer | @gridColumns = 8 | Number of columns | -        |

```less|css
.column-pull(2);

---

position: relative;
right: 25%;
```

```less|css
.column-push(3; 4);

---

left: 75%;
position: relative;
```

### Column Offset

| Variable | Type       | Default           | Description                | Required |
|----------|------------|-------------------|----------------------------|----------|
| spaced   | keyword    | -                 | Set margin between columns | -        |
| @share   | integer    | -                 | Column span                | ✔        |
| @columns | integer    | @gridColumns = 8  | Number of columns          | -        |
| @margin  | percentage | (@gridMargin / 2) | Left margin                | -        |

 ```less|css
.column-offset(2; 4);

---

margin-left: 50%;
```

```less|css
.column-offset(spaced; 1; 3; 0.02);

---

margin-left: 33.33%;
```

## hidden

```less|css
.hidden();

---

visibility: hidden;
```

## hide

```less|css
.hide();

---

display: none;
```

## Inline Grid

### Inline Row

| Variable       | Type       | Default          | Description         | Required |
|----------------|------------|------------------|---------------------|----------|
| @margin        | percentage | @gridMargin = 5% | Left margin         | -        |
| @gridSpaceless | boolean    | @gridMargin = 5% | Add whitespace hack | -        |

```less|css
.selector {
    .inline-row(2%);
}

---

.selector {
    margin-left: -2%;
    max-width: 102%;
    letter-spacing: -.32em;
}
```

### Inline Column

| Variable       | Type    | Default          | Description                | Required |
|----------------|---------|------------------|----------------------------|----------|
| spaced         | keyword | -                | Set margin between columns | -        |
| @share         | integer | -                | Column span                | ✔        |
| @columns       | integer | @gridColumns = 8 | Number of columns          | -        |
| @gridSpaceless | boolean | @gridMargin = 5% | Add whitespace hack        | -        |

```less|css
.inline-column(2; 3);

---

width: 66.66666667%;
display: inline-block;
vertical-align: top;
```

```less|css
.inline-column(spaced; 2; 3; 2%);

---

margin-left: 2%;
width: 64.66666667%;
display: inline-block;
vertical-align: top;
```

## Line Height

| Variable | Type | Default                                              | Description | Required |
|----------|------|------------------------------------------------------|-------------|----------|
| @value   | unit | [@baseLineHeight](/docs/v3/styles/variables?id=base) | Line Height | -        |

```less|css
.line-height(1.2);

---

line-height: 1.2em;
```

The default unit is em. To use a different unit update the @defaultLineHeightUnit variable in the variables file.

## lineThrough

```less|css
.line-through();

---

text-decoration: line-through;
```

## Lists

### Line List

```less|css
.inline-list();

---

li {
    display: inline;
}
```

| Variable | Type | Default | Description | Required |
|----------|------|---------|-------------|----------|
| @spacing | unit | -       | Left margin | -        |

```less|css
.inline-list(2);

---

li {
    display: inline;
    margin-left: 2;
}
li:first-child {
    margin-left: 0;
}
```

| Variable | Type   | Default | Description  | Required |
|----------|--------|---------|--------------|----------|
| @content | string | -       | Content      | -        |
| @margin  | unit   | 0       | Right margin | -        |

```less|css
.inline-list('foo'; 2px);

---

li {
    display: inline;
    margin-right: 2px;
}
li:before {
    content: 'foo';
    margin-right: 2px;
}
li:first-child:before {
    display: none;
}
```

### List Style

| Variable | Type       | Default | Description      | Required |
|----------|------------|---------|------------------|----------|
| @value   | keyword(s) | -       | List-style rules | ✔        |

```less|css
.list-style(circle inside);

---

list-style: circleinside;
```

### List Position

| Variable | Type    | Default | Description         | Required |
|----------|---------|---------|---------------------|----------|
| @value   | keyword | outside | List-style position | -        |

```less|css
.list-position(inside);
```

```
list-style-position: inside;
```

### Unstyled

```less|css
.unstyled();

---

list-style: none;
```

## lowercase

```less|css
.lowercase();

---

text-transform: lowercase;
```

## Margin

| Variable | Type | Default | Description  | Required |
|----------|------|---------|--------------|----------|
| @value   | unit | -       | Margin value | ✔        |

```less|css
.margin(5);

---

margin: 5rem;
```

| Variable                 | Type    | Default | Description  | Required |
|--------------------------|---------|---------|--------------|----------|
| top, right, bottom, left | keyword | -       | Side presets | ✔        |
| @value                   | unit    | -       | Margin value | -        |

```less|css
.margin(left; 2);

---

margin-left: 2rem;
```

| Variable             | Type    | Default | Description                   | Required |
|----------------------|---------|---------|-------------------------------|----------|
| horizontal, vertical | keyword | -       | Horizontal or vertical preset | ✔        |
| @value               | unit    | -       | Margin value                  | -        |

```less|css
.margin(vertical; 2);

---

margin-top: 2rem;
margin-bottom: 2rem;
```

| Variable             | Type    | Default | Description                   | Required |
|----------------------|---------|---------|-------------------------------|----------|
| horizontal, vertical | keyword | -       | Horizontal or vertical preset | ✔        |
| @left, @top          | unit    | -       | Margin value                  | -        |
| @right, @bottom      | unit    | -       | Margin value                  | -        |

```less|css
.margin(horizontal; 2; 3);

---

margin-left: 2rem;
margin-right: 3rem;
```

| Variable | Type | Default | Description        | Required |
|----------|------|---------|--------------------|----------|
| @y       | unit | -       | Vertical margins   | -        |
| @x       | unit | -       | Horizontal margins | -        |

```less|css
.margin(2; 3);

---

margin-top: 2rem;
margin-right: 3rem;
margin-bottom: 2rem;
margin-left: 3rem;
```

| Variable | Type | Default | Description   | Required |
|----------|------|---------|---------------|----------|
| @top     | unit | -       | Top margin    | -        |
| @right   | unit | -       | Right margin  | -        |
| @bottom  | unit | -       | Bottom margin | -        |
| @left    | unit | -       | Left margin   | -        |

```less|css
.margin(2; 3; 3; 4);

---

margin-top: 2rem;
margin-right: 3rem;
margin-bottom: 3rem;
margin-left: 4rem;
```

## Multiple Columns

| Variable | Type    | Default                                                 | Description       | Required |
|----------|---------|---------------------------------------------------------|-------------------|----------|
| @count   | integer | 2                                                       | Column width      | -        |
| @gap     | unit    | -                                                       | Column gap        | -        |
| @style   | keyword | [@gridColumns](/docs/v3/styles/variables?id=layout) = 8 | Column rule style | -        |
| @width   | unit    | [@gridMargin](/docs/v3/styles/variables?id=layout) = 5% | Column width      | -        |

```less|css
.columns(3; 2);

---

-moz-column-count: 3;
-webkit-column-count: 3;
column-count: 3;
-moz-column-gap: 2rem;
-webkit-column-gap: 2rem;
column-gap: 2rem;
```

### Column Count

| Variable | Type    | Default | Description  | Required |
|----------|---------|---------|--------------|----------|
| @value   | integer | -       | Column count | ✔        |

```less|css
.columns-count(2);

---

-moz-column-count: 2;
-webkit-column-count: 2;
column-count: 2;
```

### Column Gap

| Variable | Type | Default | Description      | Required |
|----------|------|---------|------------------|----------|
| @value   | unit | -       | Column gap width | ✔        |

```less|css
.columns-gap(1);

---

-moz-column-gap: 1rem;
-webkit-column-gap: 1rem;
column-gap: 1rem;
```

### Column Style

| Variable | Type    | Default | Description  | Required |
|----------|---------|---------|--------------|----------|
| @value   | keyword | -       | Column style | ✔        |

```less|css
.columns-style(dotted);

---

-moz-column-rule-style: dotted;
-webkit-column-rule-style: dotted;
column-rule-style: dotted;
```

### Column Width

| Variable | Type    | Default | Description  | Required |
|----------|---------|---------|--------------|----------|
| @value   | integer | -       | Column width | ✔        |

```less|css
.columns-width(20);

---

-moz-column-rule-width: 20rem;
-webkit-column-rule-width: 20rem;
column-rule-width: 20rem;
```

## noClear

```less|css
.no-clear();

---

&::-ms-clear {
    display: none
}
&::-webkit-search-cancel-button {
    -webkit-appearance: none
}
```

## Opacity

| Variable | Type | Default | Description | Required |
|----------|------|---------|-------------|----------|
| @value   | unit | -       | Opacity     | ✔        |

```less|css
.opacity(50%);

---

filter: alpha(opacity=50);
opacity: 0.5;
```

### Transparent

```less|css
.transparent();

filter: alpha(opacity=0);
opacity: 0;
```

### Opaque

```less|css
.opaque();
---

filter: alpha(opacity=100);
opacity: 1;
```

## Other

### Resize

| Variable | Type    | Default | Description  | Required |
|----------|---------|---------|--------------|----------|
| @value   | keyword | -       | Resize value | ✔        |

```less|css
.resize(horizontal);

---

resize: horizontal;
```

### Resizable

| Variable | Type    | Default | Description  | Required |
|----------|---------|---------|--------------|----------|
| @value   | keyword | both    | Resize value | -        |

```less|css
.resizable(vertical);

---

overflow: hidden;
resize: vertical;
```

### Hide Text

```less|css
.hide-text();

---

overflow: hidden;
text-indent: 100%;
white-space: nowrap;
```

### Selection

| Variable    | Type                   | Default                                                                         | Description          | Required |
|-------------|------------------------|---------------------------------------------------------------------------------|----------------------|----------|
| @color      | color                  | [@selectionColor](/docs/v3/styles/variables?id=miscellaneous) = @white          | Selection color      | -        |
| @background | color, string, keyword | [@selectionBackground](/docs/v3/styles/variables?id=miscellaneous) = @linkColor | Selection background | -        |

```less|css
.selection();

---

::-moz-selection {
    text-shadow: none;
    background: #167da3;
    color: #ffffff;
}
::selection {
    text-shadow: none;
    background: #167da3;
    color: #ffffff;
}
```

### Cursor
| Variable | Type    | Default | Description  | Required |
|----------|---------|---------|--------------|----------|
| @value   | keyword | pointer | Cursor value | -        |

```less|css
.cursor();

---

cursor: pointer;
```

### Overflow

| Variable | Type    | Default | Description    | Required |
|----------|---------|---------|----------------|----------|
| x, y     | keyword | -       | Overflow axis  | -        |
| @value   | keyword | -       | Overflow value | ✔        |

```less|css
.overflow(hidden);

---

overflow: hidden;
```

```less|css
.overflow(x; scroll);

---

overflow-x: scroll;
```

| Variable | Type    | Default | Description      | Required |
|----------|---------|---------|------------------|----------|
| @x       | keyword | -       | Overflow-x value | -        |
| @y       | keyword | -       | Overflow-y value | -        |

```less|css
.overflow(hidden; scroll);

---

overflow-x: hidden;
overflow-y: scroll;
```

### Crop & Scroll

| Variable             | Type    | Default | Description                   | Required |
|----------------------|---------|---------|-------------------------------|----------|
| horizontal, vertical | keyword | -       | Horizontal or vertical preset | -        |
| @value               | keyword | true    | Overflow value                | -        |

```less|css
.crop(both);

---

overflow: hidden;
```

```less|css
.crop(vertical);

---

overflow-y: hidden;
```

```less|css
.scroll();

---

overflow: scroll;
```

```less|css
.scroll(horizontal);

---

overflow-x: scroll;
```

### Fill

| Variable                   | Type           | Default | Description                          | Required |
|----------------------------|----------------|---------|--------------------------------------|----------|
| horizontal, vertical, both | keyword        | -       | Horizontal, vertical, or both preset | -        |
| @value                     | keyword, color | true    | Fill value                           | -        |

```less|css
.fill(horizontal);

---

width: 100%;
```

```less|css
.fill(blue);

---

fill: #00f;
```

```less|css
.fill(both);

---

width: 100%;
height: 100%;
```

### No Clear

```less|css
.no-clear();

---

::-ms-clear {
    display: none;
}
::-webkit-search-cancel-button {
    -webkit-appearance: none;
}
```

## Padding

| Variable | Type | Default | Description   | Required |
|----------|------|---------|---------------|----------|
| @value   | unit | -       | Padding value | ✔        |

```less|css
.padding(5);

---

padding: 5rem;
```

| Variable                 | Type    | Default | Description   | Required |
|--------------------------|---------|---------|---------------|----------|
| top, right, bottom, left | keyword | -       | Side presets  | ✔        |
| @value                   | unit    | -       | Padding value | ✔        |

```less|css
.padding(left; 2);

---

padding-left: 2rem;
```

| Variable   | Type    | Default | Description                    | Required |
|------------|---------|---------|--------------------------------|----------|
| horizontal | keyword | -       | Sets padding to @bumperPadding | ✔        |

```less|css
.padding(horizontal);

---

padding-left: 6%;
padding-right: 6%;
```

| Variable             | Type    | Default | Description                   | Required |
|----------------------|---------|---------|-------------------------------|----------|
| horizontal, vertical | keyword | -       | Horizontal or vertical preset | ✔        |
| @value               | unit    | -       | Padding value                 | ✔        |

```less|css
.padding(vertical; 2);

---

padding-top: 2rem;
padding-bottom: 2rem;
```

| Variable             | Type    | Default | Description                   | Required |
|----------------------|---------|---------|-------------------------------|----------|
| horizontal, vertical | keyword | -       | Horizontal or vertical preset | ✔        |
| @left, @top          | unit    | -       | Left or top padding value     | ✔        |
| @right, @bottom      | unit    | -       | Right or bottom padding value | ✔        |

```less|css
.padding(horizontal; 2; 3);

---

padding-left: 2rem;
padding-right: 3rem;
```

| Variable    | Type | Default | Description      | Required |
|-------------|------|---------|------------------|----------|
| @vertical   | unit | -       | Vertical padding | ✔        |
| @horizontal | unit | -       | Horizontal       | ✔        |

```less|css
.padding(2; 3);

---

padding-top: 2rem;
padding-right: 3rem;
padding-bottom: 2rem;
padding-left: 3rem;
```

| Variable | Type | Default | Description    | Required |
|----------|------|---------|----------------|----------|
| @top     | unit | -       | Top padding    | ✔        |
| @right   | unit | -       | Right padding  | ✔        |
| @bottom  | unit | -       | Bottom padding | ✔        |
| @left    | unit | -       | Left padding   | ✔        |

```less|css
.padding(2; 3; 3; 4);

---

padding-top: 2rem;
padding-right: 3rem;
padding-bottom: 3rem;
padding-left: 4rem;
```

| Variable | Type | Default                                                    | Description   | Required |
|----------|------|------------------------------------------------------------|---------------|----------|
| @padding | unit | [@bumperPadding](/docs/v3/styles/variables?id=layout) = 6% | Padding value | -        |

### Padded

```less|css
.padded(2%);

---

padding-left: 2%;
padding-right: 2%;
```

## Position

### Top, Right, Bottom & Left

| Variable | Type | Default | Description | Required |
|----------|------|---------|-------------|----------|
| @value   | unit | 0       | Amount      | -        |

```less|css
.top(4);

---

top: 4rem;
```

```less|css
.right(2);

---

right: 2rem;
```

### Position

| Variable | Type    | Default | Description | Required |
|----------|---------|---------|-------------|----------|
| @value   | keyword | -       | Positioning | ✔        |
| @top     | unit    | -       | Top         | -        |
| @right   | unit    | -       | Right       | -        |
| @bottom  | unit    | -       | Bottom      | -        |
| @left    | unit    | -       | Left        | -        |

```less|css
.position(fixed; 4px; 3; 2%; 1rem);

---

position: fixed;
top: 4px;
right: 3rem;
bottom: 2%;
left: 1rem;
```

### Absolute & Fixed

| Variable | Type | Default | Description     | Required |
|----------|------|---------|-----------------|----------|
| @top     | unit | -       | Top position    | -        |
| @right   | unit | -       | Right position  | -        |
| @bottom  | unit | -       | Bottom position | -        |
| @left    | unit | -       | Left position   | -        |

```less|css
.absolute();

---

position: absolute;
```

```less|css
.absolute(3; 2);

---

position: absolute;
top: 3rem;
right: 2rem;
```

```less|css
.fixed(2rem);

---

position: fixed;
top: 2rem;
```

### Relative

```less|css
.relative();

---

position: relative;
```

### Static

```less|css
.static();

---

position: static;
```

### Z-Index

| Variable | Type    | Default | Description | Required |
|----------|---------|---------|-------------|----------|
| @index   | integer | 1       | Z-Index     | -        |

```less|css
.z-index(4);

---

z-index: 4;
```

## Responsive

### Media Query

| Variable  | Type  | Default | Description              | Required |
|-----------|-------|---------|--------------------------|----------|
| @maxWidth | unit  | -       | Breakpoint maximum width | ✔        |
| @rules    | rules | -       | CSS rules                | ✔        |

```less|css
.selector {
    .media-query(500px; {
        .color(red);
    });
}

---

@media (max-width: 500px) {
    .selector {
        color: #f00;
    }
}
```

## right

```less|css
.right();

---

float: right;
```

```less|css
.right(4);

---

right: 4rem;
```

## Rounded Corners

| Variable | Type | Default                                                            | Description    | Required |
|----------|------|--------------------------------------------------------------------|----------------|----------|
| @value   | unit | [@defaultRadius](/docs/v3/styles/variables?id=miscellaneous) = 3px | Size of radius | -        |

```
.rounded(3);
```

```
background-clip: border-box;
border-radius: 3rem;
```

| Variable                 | Type    | Default                                                            | Description  | Required |
|--------------------------|---------|--------------------------------------------------------------------|--------------|----------|
| top, right, bottom, left | keyword | -                                                                  | Side presets | ✔        |
| @value                   | unit    | [@defaultRadius](/docs/v3/styles/variables?id=miscellaneous) = 3px | Radius       | -        |

```less|css
.rounded(top);

---

background-clip: border-box;
border-top-left-radius: 3px;
border-top-right-radius: 3px;
```

```less|css
.rounded(right; 5);

---

background-clip: border-box;
border-top-right-radius: 5rem;
border-bottom-right-radius: 5rem;
```

| Variable    | Type    | Default                                                            | Description          | Required |
|-------------|---------|--------------------------------------------------------------------|----------------------|----------|
| top, bottom | keyword | -                                                                  | Top or bottom preset | ✔        |
| left, right | keyword | -                                                                  | Left or right preset | ✔        |
| @value      | unit    | [@defaultRadius](/docs/v3/styles/variables?id=miscellaneous) = 3px | Radius               | -        |

```less|css
.rounded(bottom; left);

---

background-clip: border-box;
border-bottom-left-radius: 3px;
```

```less|css
.rounded(top; right; 4);

---

background-clip: border-box;
border-top-right-radius: 4rem;
```

| Variable | Type | Default | Description   | Required |
|----------|------|---------|---------------|----------|
| @top     | unit | -       | Top radius    | ✔        |
| @right   | unit | -       | Right radius  | ✔        |
| @bottom  | unit | -       | Bottom radius | ✔        |
| @left    | unit | -       | Left radius   | ✔        |

```less|css
.rounded(2px; 3rem; 4px; 5px);

---

background-clip: border-box;
border-top-left-radius: 2px;
border-top-right-radius: 3rem;
border-bottom-right-radius: 4px;
border-bottom-left-radius: 5px;
```

## sepia

```less
.sepia(value = 0.5);
```

```less|css
.sepia(1);

---

filter: sepia(1);
```

## Shapes

### Caret

| Variable                       | Type    | Default                                                                  | Description                 | Required |
|--------------------------------|---------|--------------------------------------------------------------------------|-----------------------------|----------|
| up, down, right, left          | keyword | -                                                                        | Direction                   | ✔        |
| @color                         | color   | [@darkGray](/docs/v3/styles/variables?id=grayscale) = lighten(#000, 45%) | Color                       | -        |
| @size                          | unit    | 5px                                                                      | Size                        | -        |
| @horizontalSize, @verticalSize | unit    | @size                                                                    | Horizontal or vertical size | -        |

```less|css
.caret(up; red; 10px);

---

content: ' ';
height: 0;
width: 0;
border-left: 10pxsolidtransparent;
border-right: 10pxsolidtransparent;
border-bottom: 10pxsolid#ff0000;
```

```less|css
.caret(left; blue);

---

content: ' ';
height: 0;
width: 0;
border-bottom: 5pxsolidtransparent;
border-top: 5pxsolidtransparent;
border-right: 5pxsolid#0000ff;
```

## show

```less|css
.show();

---

display: inherit;
```

## Sizing

| Variable              | Type | Default | Description     | Required |
|-----------------------|------|---------|-----------------|----------|
| @value                | unit | -       | Width or Height | ✔        |
| @maxWidth, @maxHeight | unit | -       | Maximum         | -        |

```less|css
.width(4; 5);
.height(3; 40%);

---

width: 4rem;
max-width: 5rem;
height: 3rem;
max-height: 40%;
```

| Variable | Type | Default | Description        | Required |
|----------|------|---------|--------------------|----------|
| @value   | unit | -       | Minimum or maximum | ✔        |

```less|css
.max-width(4rem);
.min-width(2rem);

---

max-width: 4rem;
min-width: 2rem;
```

```less|css
.max-height(5rem);
.min-height(3rem);

---

max-height: 5rem;
min-height: 3rem;
```

### Size

| Variable | Type | Default | Description           | Required |
|----------|------|---------|-----------------------|----------|
| @width   | unit | -       | Width or Width/Height | ✔        |
| @height  | unit | -       | Height                | -        |

```less|css
.size(15);
.size(100px; 6);

---

height: 15rem;
width: 15rem;

height: 6rem;
width: 100px;
```

```less|css
.min-size(12);
.min-size(2; 3);

.max-size(20);
.max-size(4; 5);

---

min-height: 12rem;
min-width: 12rem;

min-height: 3rem;
min-width: 2rem;

max-height: 20rem;
max-width: 20rem;

max-height: 5rem;
max-width: 4rem;
```

### Square

| Variable | Type | Default | Description    | Required |
|----------|------|---------|----------------|----------|
| @size    | unit | -       | Width & height | ✔        |

```less|css
.square(50px);

---

height: 50px;
width: 50px;
```

### Ratio

| Variable | Type    | Default | Description | Required |
|----------|---------|---------|-------------|----------|
| embed    | keyword | -       | Embed       | -        |
| @ratio   | unit    | (16/9)  | Ratio       | -        |

```less|css
.ratio((4 / 3));

---

display: block;
height: 0;
padding-top: 75%;
```

```less|css
.selector {
    .ratio(embed; (16 / 9));
}

---

.selector {
    overflow: hidden;
    position: relative;
}
.selector:before {
    content: ' ';
    display: block;
    height: 0;
    padding-top: 56.25%;
}
```

### Circle

| Variable  | Type          | Default | Description   | Required |
|-----------|---------------|---------|---------------|----------|
| @diameter | unit          | -       | Diameter      | ✔        |
| @crop     | boolean       | false   | Crop          | -        |
| @display  | block, inline | block   | Display value | -        |

```less|css
.circle(10px; true);

---

display: block;
height: 10px;
background-clip: border-box;
border-radius: 5px;
width: 10px;
overflow: hidden;
```

## SVG

### Fill

| Variable | Type  | Default                                                     | Description | Required |
|----------|-------|-------------------------------------------------------------|-------------|----------|
| @color   | color | [@baseColor](/docs/v3/styles/variables#base) = @darkestGray | Color value | -        |
| @value   | unit  | -                                                           | Opacity     | -        |

```less|css
.fill(#123);

---

fill: #123;
```

```less|css
.fill(red; 50%);

---

fill: rgba(155, 155, 155, .5);
```

### Fill Dark/Light

| Variable    | Type    | Default                                                         | Description          | Required |
|-------------|---------|-----------------------------------------------------------------|----------------------|----------|
| light, dark | keyword | -                                                               | Light or dark preset | ✔        |
| @opacity    | unit    | [@defaultOpacity](/docs/v3/styles/variables#miscellaneous) = .2 | Fill opacity         | -        |

```less|css
.fill(light);

---

fill: rgba(255, 255, 255, .2);
```

```less|css
.fill(dark; 25%);

---

fill: rgba(0, 0, 0, .25);
```

### Stroke

| Variable | Type  | Default                                                    | Description  | Required |
|----------|-------|------------------------------------------------------------|--------------|----------|
| @color   | color | [@baseColor](/docs/v3/style/variables#base) = @darkestGray | Color value  | -        |
| @width   | unit  | -                                                          | Stroke width | -        |

```less|css
.stroke(#123);

---

stroke: #123;
```

```less|css
.stroke(red; 2px);

---

stroke: red 2px;
```

## Tables

### Responsive Table

```less|css
.selector {
    .responsive-table();
}

---

.selectoroverflow-x: auto;
    overflow-y: hidden;
    width: 100%;
    margin-bottom: 4rem;
    table {
        margin-bottom: 0;
    }
}
```

## Text Shadows

| Variable | Type            | Default                                      | Description       | Required |
|----------|-----------------|----------------------------------------------|-------------------|----------|
| @value   | string, keyword | '1px 1px 0 rgba(0, 0, 0, @{defaultOpacity})' | Text shadow rules | -        |

```less|css
.text-shadow('2px 1px 0 #000');

---

text-shadow: 2px 1px 0 #000;
```

| Variable | Type    | Default | Description       | Required |
|----------|---------|---------|-------------------|----------|
| inner    | keyword | -       | Inner preset      | -        |
| @color   | color   | -       | Shadow color      | ✔        |
| @x       | value   | 1px     | Horizontal offset | -        |
| @y       | value   | 1px     | Vertical offset   | -        |
| @blur    | value   | 0       | Blur distance     | -        |

```less|css
.text-shadow(blue; 4px; 3px; 2px);

---

text-shadow: 4px 3px 2px#00f;
```

```less|css
.text-shadow(inner; blue);

---

.text-shadow(inner; blue);
```

| Variable         | Type    | Default                                                         | Description          | Required |
|------------------|---------|-----------------------------------------------------------------|----------------------|----------|
| inner            | keyword | -                                                               | Inner preset         | -        |
| light, dark      | keyword | -                                                               | Light or dark preset | ✔        |
| @value, @opacity | number  | [@defaultOpacity](/docs/v3/styles/variables#miscellaneous) = .2 | Opacity              | -        |
| @x               | unit    | 1px                                                             | Horizontal offset    | -        |
| @y               | unit    | 1px                                                             | Vertical offset      | -        |
| @blur            | unit    | 0                                                               | Blur                 | -        |

```less|css
.text-shadow(light; 0.4);

---

text-shadow: 1px 1px 0 rgba(255, 255, 255, 0.4);
```

```less|css
.text-shadow(inner; dark; 50%);

---

text-shadow: -1px-1px 0 rgba(0, 0, 0, 0.5);
```

## Text Styling

### Text Sharpen

```less|css
.text-sharpen();

---

-moz-osx-font-smoothing: grayscale;
-webkit-font-smoothing: antialiased;
font-smoothing: antialiased;
```

### Capitalize

```less|css
.capitalize();

---

text-transform: capitalize;
```

### Lowercase

```less|css
.lowercase();

---

text-transform: lowercase;
```

### Uppercase

```less|css
.uppercase();

---

text-transform: uppercase;
```

### Text Transform

| Variable | Type    | Default | Description          | Required |
|----------|---------|---------|----------------------|----------|
| @value   | keyword | none    | Text transform rules | -        |

```less|css
.text-transform(uppercase);

---

text-transform: uppercase;
```

### Wrap

```less|css
.wrap();

---

white-space: initial;
```

### No-Wrap

```less|css
.no-wrap();

---

white-space: nowrap;
```

### Ellipsis

| Variable  | Type    | Default | Description               | Required |
|-----------|---------|---------|---------------------------|----------|
| @maxWidth | keyword | -       | Maximum width for element | -        |

```less|css
.ellipsis(20);

---

overflow-x: hidden;
text-overflow: ellipsis;
white-space: nowrap;
max-width: 20rem;
```

### Underline

```less|css
.underline();

---

text-decoration: underline;
```

| Variable | Type    | Default | Description           | Required |
|----------|---------|---------|-----------------------|----------|
| @style   | keyword | -       | Text decoration style | ✔        |
| @color   | color   | inheret | Text decoration color | -        |

```less|css
.underline(solid; white);

---

text-decoration: underline;
-moz-text-decoration-line: underline;
-moz-text-decoration-style: solid;
-moz-text-decoration-color: #fff;
text-decoration: #fffsolidunderline;
```

### Line-Through

```less|css
.line-through();

---

text-decoration: line-through;
```

### Text Decoration

| Variable | Type    | Default   | Description           | Required |
|----------|---------|-----------|-----------------------|----------|
| @value   | keyword | underline | Text decoration rules | -        |

```less|css
.text-decoration(overline);

---

text-decoration: overline;
```

| Variable | Type    | Default | Description | Required |
|----------|---------|---------|-------------|----------|
| @line    | keyword | -       | Line type   | ✔        |
| @style   | keyword | -       | Line style  | ✔        |
| @color   | color   | inheret | Line color  | -        |

```less|css
.text-decoration(underline; dotted; blue);

---

text-decoration: underline;
-moz-text-decoration-line: underline;
-moz-text-decoration-style: dotted;
-moz-text-decoration-color: #00f;
text-decoration: #00fdottedunderline;
```

### Outline

| Variable | Type    | Default       | Description           | Required |
|----------|---------|---------------|-----------------------|----------|
| @value   | keyword | 'thin dotted' | Element outline rules | -        |

```less|css
.outline();

---

outline: thindotted;
```

### Text Overflow

| Variable | Type    | Default | Description                 | Required |
|----------|---------|---------|-----------------------------|----------|
| @value   | keyword | -       | Element text overflow value | -        |

```less|css
.text-overflow(clip);

---

text-overflow: clip;
```

### Text Overflow

| Variable | Type    | Default | Description                 | Required |
|----------|---------|---------|-----------------------------|----------|
| @value   | keyword | -       | Element text overflow value | -        |

```less|css
.text-overflow(clip);

---

text-overflow: clip;
```

### White Space

| Variable | Type    | Default | Description               | Required |
|----------|---------|---------|---------------------------|----------|
| @value   | keyword | -       | Element white space value | -        |

```less|css
.white-space(initial);

---

white-space: initial;
```

### Letter Spacing

| Variable | Type | Default | Description          | Required |
|----------|------|---------|----------------------|----------|
| @value   | unit | -       | Letter kerning rules | ✔        |

```less|css
.letter-spacing(2);

---

letter-spacing: 2rem;
```

### Word Spacing

| Variable | Type | Default | Description        | Required |
|----------|------|---------|--------------------|----------|
| @value   | unit | -       | Word spacing rules | ✔        |

```less|css
.word-spacing(3);

---

word-spacing: 3rem;
```

### Text Indent

| Variable | Type | Default | Description          | Required |
|----------|------|---------|----------------------|----------|
| @value   | unit | -       | Text indention rules | ✔        |

```less|css
.text-indent(1rem);

---

text-indent: 1rem;
```

### User Select

| Variable | Type    | Default | Description                  | Required |
|----------|---------|---------|------------------------------|----------|
| @value   | keyword | none    | Controls selection operation | -        |

```less|css
.user-select(text);

---

-moz-user-select: text;
-ms-user-select: text;
-webkit-user-select: text;
user-select: text;
```

### Tab Size

| Variable | Type    | Default                                                   | Description | Required |
|----------|---------|-----------------------------------------------------------|-------------|----------|
| @value   | integer | [@codeBlockTabSize](/docs/v3/style/variables?id=code) = 4 | Tab length  | -        |

```less|css
.tab-size(4);

---

-moz-tab-size: 4;
tab-size: 4;
```

## textSharpen

```less|css
.textSharpen();

---
font-smoothing: antialiased;
```

## Transforms

### Transform

| Variable   | Type    | Default | Description     | Required |
|------------|---------|---------|-----------------|----------|
| @arguments | keyword | -       | Transform rules | ✔        |

```less|css
.transform(translateX(10px));

---

-ms-transform: translateX(10px);
-webkit-transform: translateX(10px);
transform: translateX(10px);
```

### Rotate

| Variable | Type    | Default | Description | Required |
|----------|---------|---------|-------------|----------|
| @angle   | integer | 45      | Angle       | -        |

```less|css
.rotate(30);

---

-ms-transform: rotate(30deg);
-webkit-transform: rotate(30deg);
transform: rotate(30deg);
```

### Scale

| Variable     | Type             | Default | Description        | Required |
|--------------|------------------|---------|--------------------|----------|
| @value, x, y | integer, keyword | 1       | Scale or dimension | -        |
| @value       | integer          | 1       | Scale              | -        |

```less|css
.scale(x; 2);

---

-ms-transform: scaleX(2);
-webkit-transform: scaleX(2);
transform: scaleX(2);
```

### Skew

| Variable | Type    | Default | Description     | Required |
|----------|---------|---------|-----------------|----------|
| @x       | integer | 45      | Horizontal skew | -        |
| @y       | integer | 0       | Vertical skew   | -        |

```less|css
.skew(30, 15);

---

-ms-transform: skew(30deg, 15deg);
-webkit-transform: skew(30deg, 15deg);
transform: skew(30deg, 15deg);
```

| Variable | Type    | Default | Description   | Required |
|----------|---------|---------|---------------|----------|
| x, y     | keyword | -       | X or Y preset | ✔        |
| @x, @y   | integer | 45      | Vertical skew | -        |

```less|css
.skew(y; 15);

---

-ms-transform: skewY(15deg);
-webkit-transform: skewY(15deg);
transform: skewY(15deg);
```

### Transform Origin

| Variable | Type    | Default | Description     | Required |
|----------|---------|---------|-----------------|----------|
| @x       | integer | -       | Horizontal      | ✔        |
| @y       | integer | 0       | Vertical origin | -        |

```less|css
.transform-origin(15%; 10%);

---

-ms-transform: transform-origin(15%, 10%);
-webkit-transform: transform-origin(15%, 10%);
transform: transform-origin(15%, 10%);
```

### Translate

| Variable | Type    | Default | Description   | Required |
|----------|---------|---------|---------------|----------|
| @x       | integer | 0       | X translation | -        |
| @y       | integer | 0       | Y translation | -        |
| @z       | integer | -       | Z translation | -        |

```less|css
.translate(10px; 15px; 20%);

---

-webkit-transform: translate3d(10px, 15px, 20%);
transform: translate3d(10px, 15px, 20%);
```

## Transitions

### Transition

| Variable | Type   | Default                   | Description      | Required |
|----------|--------|---------------------------|------------------|----------|
| @value   | string | 'all 0.2s ease-in-out 0s' | Transition rules | ✔        |

```less|css
.transition('all 4s ease-in 1s');

---

-webkit-backface-visibility: hidden;
-webkit-transition: all 4sease-in 1s;
transition: all 4sease-in 1s;
```

| Variable  | Type    | Default                                                             | Description         | Required |
|-----------|---------|---------------------------------------------------------------------|---------------------|----------|
| @property | keyword | all                                                                 | Animatable Property | -        |
| @duration | seconds | [@defaultDuration](/docs/v3/style/variables?id=miscellaneous) = .2s | Duration            | -        |
| @ease     | keyword | ease-in-out                                                         | Timing function     | -        |
| @delay    | seconds | 0s                                                                  | Delay               | -        |

```less|css
.transition(all; 2s; ease-in; 0.2s);

---

-webkit-backface-visibility: hidden;
-webkit-transition: all 2sease-in 0.2s;
transition: all 2sease-in 0.2s;
```

### Transition Delay

| Variable | Type    | Default | Description | Required |
|----------|---------|---------|-------------|----------|
| @delay   | seconds | 1s      | Delay value | -        |

```less|css
.transition-delay(3s);

---

-webkit-transition-delay: 3s;
transition-delay: 3s;
```

### Transition Duration

| Variable  | Type    | Default                                                             | Description    | Required |
|-----------|---------|---------------------------------------------------------------------|----------------|----------|
| @duration | seconds | [@defaultDuration](/docs/v3/style/variables?id=miscellaneous) = .2s | Duration value | -        |

```less|css
.transition-duration(0.5s);

---

-webkit-transition-duration: 0.5s;
transition-duration: 0.5s;
```

## unstyled

```less|css
.unstyled();

---

list-style: none;
```

## uppercase

```less|css
.uppercase();

---

text-transform: uppercase;
```

## visible

```less|css
.visible();

---

visibility: visible;
```

## wrap

```less|css
.wrap();

---

white-space: normal;
```