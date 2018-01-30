## absolute

```scss
@mixin absolute($top: false, $right: false, $bottom: false, $left: false)
```

```scss|css
@include absolute();

---

position: absolute;
```

```scss|css
@include absolute(4rem, 3rem, 2rem, 1rem);

---

position: absolute;
top: 4rem;
right: 3rem;
bottom: 2rem;
left: 1rem;
```

```scss|css
@include absolute(4rem, 3rem);

---

position: absolute;
top: 4rem;
left: 3rem;
```

## block

```scss
@mixin block($width, $height);
```

```scss|css
@include block();

---

display: block;
```

```scss|css

@include block(40rem, 100px);

---

display: block;
width: 40rem;
height: 100px;
```

## bookends
```scss
@mixin bookends($value: '-', $margin: .5em, $font: false, $color: false);
```
```scss|css
@include bookends('-', .5em);

---

&:before {
    content: '-';
    margin-right: .5em;
}
&:after {
    content: '-';
    margin-left: .5em;
}
```

```scss|css
@include bookends('~', 1, $color: red);

---

&:before {
    content: '~';
    margin-right: 1rem;
    color: red;
}
&:after {
    content: '~';
    margin-left: 1rem;
    color: red;
}
```

## centeredBlock

```scss
@mixin centeredBlock($maxWidth: false, $margin: false)
```

```scss|css
@include centeredBlock();

---

display: block;
margin-left: auto;
margin-right: auto;
```

```scss|css
@include centeredBlock(80rem, 2rem);

---

display: block;
margin-left: auto;
margin-right: auto;
width: 80rem;
margin-bottom: 2rem;

```

## circle

```scss
@mixin circle($diameter, $crop: false, $display: block)
```

```scss|css
@include circle(.5);

---

background-clip: border-box;
border-radius: 0.25rem;
height: 0.5rem;
width: 0.5rem;
display: block;
```

```scss|css
@include circle(.5, true);

---
background-clip: border-box;
border-radius: 0.25rem;
height: 0.5rem;
width: 0.5rem;
overflow: hidden;
display: block;
```

```scss|css
@include circle(.5, $display: inline);

---

background-clip: border-box;
border-radius: 0.25rem;
height: 0.5rem;
width: 0.5rem;
display: inline-block;

```

## clearfix

```scss|css
@include clearfix();

---

&:after {
    clear: both;
    content: '';
    display: block;
}
```

## column

```scss
@mixin column($keyword: false, $share: false, $columns: $gridColumns, $margin: $gridMargin)
```

```scss|css
@include column();

---

float: left;
width: 100%;
```

```scss|css
@include column(40%);

---

float: left;
width: 40%;
```
```scss|css
@include column(spaced, 1, 4, 2%);

---

float: left;
margin-left: 2%;
width: 23%;
```

```scss|css
@include column(1, 2);

---

float: left;
width: 50%;
```

## columnModify

```scss
@mixin columnModify($keyword: false, $share: false, $columns: $gridColumns, $margin: $gridMargin)
```

```scss|css
@include columnModify(60%);

---

width: 60%;
```

```scss|css
@include columnModify(spaced, 1, 4, 5%);

---

margin-left: 5%;
width: -20%;
@include columnModify(1, 5);
width: 20%;
```

## columnOffset

```scss
@mixin columnOffset($keyword: false, $share: false, $columns: $gridColumns, $margin: ($gridMargin / 2))
```

```scss|css
@include columnOffset(spaced, 3, 4, 5%);

---

margin-left: 85%;
```

```scss|css
@include columnOffset(2, 5);

---

margin-left: 40%;
```

## columnPull

```scss
@mixin columnPull($share, $columns: $gridColumns)
```

```scss|css
@include columnPull(1, 2);

---

position: relative;
right: 50%;
```

## columnPush

```scss
@mixin columnPush($share, $columns: $gridColumns)
```

```scss|css
@include columnPush(1, 2);

---

left: 50%;
position: relative;
```

## columnReset

```scss
@mixin columnReset($resetMargin: false)
```

```scss|css
@include columnReset();

---

float: none;
width: auto;
```

```scss|css
@include columnReset(true);

---

float: none;
width: auto;
margin-left: 0;
```

## ellipsis

```scss
@mixin ellipsis(maxWidth = false)
```

```scss|css
@include ellipsis();

---

overflow-x: hidden;
text-overflow: ellipsis;
white-space: nowrap;
```

```scss|css
@include ellipsis(10);

---

overflow-x: hidden;
text-overflow: ellipsis;
white-space: nowrap;
max-width: 10rem;
```

## fixed

```scss
@mixin fixed($top: false, $right: false, $bottom: false, $left: false);
```

```scss|css
@include fixed();

---

position: fixed;
```

```scss|css
@include fixed($bottom: 3rem, $top: 4rem);

---

position: fixed;
top: 4rem;
bottom: 3rem;
```
## flex

```scss
@mixin flex($grow: 0, $shrink: 0, $basis: auto)
```

```scss|css
@include flex();

---

flex-grow: 0;
flex-shrink: 0;
flex-basis: auto;
```

```scss|css
@include flex(1, 2);

---
flex-grow: 1;
flex-shrink: 2;
flex-basis: auto;
```

## flexContainer

```scss
@mixin flexContainer($direction: row, $wrap: nowrap, $justify: flex-start,
$align: stretch, $alignContent: stretch)
```

```scss|css
@include flexContainer();

---

display: flex;
flex-direction: row;
flex-wrap: nowrap;
justify-content: flex-start;
align-items: stretch;
align-content: stretch;
```

```scss|css
@include flexContainer(column, wrap, $alignContent: start);

---

display: flex;
flex-direction: column;
flex-wrap: wrap;
justify-content: flex-start;
align-items: stretch;
align-content: start;
```

## font

```scss
@mixin font($family: $baseFont, $size, $weight, $lineHeight, $style, $spacing)
```

```scss|css
@include font('Times New Roman', 1.4, bold, 1.5, italic, 0.1);

---

font-family: 'Times New Roman';
font-size: 1.4rem;
font-weight: bold;
line-height: 1.5em;
letter-spacing: 0.1rem;
```

## heading

```scss
@mixin heading($fontSize: false)
```

```scss|css
@include heading();

---

color: inherit;
font-family: 'Tahoma, Geneva, sans-serif';
font-weight: bold;
line-height: 1.4em;
margin-bottom: 2rem;
small {
    font-weight: normal;
}
```

## hideText

```scss|css
@include hideText();

---

overflow: hidden;
text-indent: 110%;
white-space: nowrap;
```

## icon

```scss
@mixin icon(icon, size = 'inherit', rotate = false, weight = 'normal', height = 0, sharpen = true, font = vars.icon.family)
```

```scss|css
.block {
    &::after {
        @include icon(\e901);
    }
}

---

.block::after {
    content: '\e901';
    font-family: 'Open Sans' sans-serif;
    font-size: inherit;
    font-weight: normal;
    line-height: 0;
    font-style: normal;
    display: inline-block;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
```
## iconModify

```scss
@mixin iconModify(icon = false, size = false, rotate = false, weight = false, sharpen = false)
```

```scss|css
.block {
    &::after {
        @include iconModify(\e901);
    }
}

---

.block::after {
    content: '\e901';
}
```

## inlineBlock

```scss
@mixin inlineBlock(width, height)
```

```scss|css
@include inlineBlock();

---

display: inline-block;
```

```scss|css
@include inlineBlock(40rem, 30rem);

---

display: inline-block;
width: 40rem;
height: 30rem;
```

```scss|css
@include inlineBlock($height: 100px);

---

display: inline-block;
height: 100px;
```

## inlineColumn

```scss
@mixin inlineColumn(keyword, share, columns = vars.grid.columns, margin = vars.grid.margin, spaceless = vars.grid.spaceless)
```

```scss|css
@include inlineColumn(spaced, 1, 4, 4%);

---

display: inline-block;
vertical-align: top;
margin-left: 4%;
width: 21%;
letter-spacing: normal;
```

```scss|css
@include inlineColumn(1, 5);

---

display: inline-block;
vertical-align: top;
width: 20%;
```

## inlineRow

```scss
@mixin inlineRow(margin = vars.grid.margin, spaceless = vars.grid.spaceless)
```

```scss|css
@include inlineRow(4%, false);

---

margin-left: -4%;
max-width: 104%;
letter-spacing: -.32em;
```

```scss|css
@include inlineRow(4%, true);

---

margin-left: -4%;
max-width: 104%;
```

## loadFont

```scss
@mixin loadFont(name, $file: $name, $weight: normal, $style: normal)
```

```scss|css
@include loadFont(icomoon, $weight: 500);

---

@font-face {
    font-family: icomoon;
    font-weight: 500;
    font-style: normal;
    src: url('../fonts/icomoon.woff2'),
        url('../fonts/icomoon.woff'),
        url('../fonts/icomoon.ttf');
}
```

## noClear

```scss|css
@mixin noClear();

---

&::-ms-clear {
    display: none
}
&::-webkit-search-cancel-button {
    -webkit-appearance: none
}
```

## placeholder

```scss
@mixin placeholder($color: $inputPlaceholderColor)
```

```scss|css
@include placeholder();

---

&:-moz-placeholder {
    color: #bfbfbf
}
&::-moz-placeholder {
    color: #bfbfbf
}
&:-ms-input-placeholder {
    color: #bfbfbf
}
&::-webkit-input-placeholder {
    color: #bfbfbf
}
```

```scss|css
@include placeholder(#fff);

---

&:-moz-placeholder {
    color: #fff
}
&::-moz-placeholder {
    color: #fff
}
&:-ms-input-placeholder {
    color: #fff
}
&::-webkit-input-placeholder {
    color: #fff
}
```

## prefix

```scss
@mixin prefix($value: '-', $margin: .5em, $font: false, $color: false)
```

```scss|css
@include prefix();

---

&:before {
    content: '-';
    margin-right: .5em;
}
prefix('~', 1rem, $color: blue);
&:before {
    content: '~';
    margin-right: 1rem;
    color: blue;
}
```

## ratio

```scss
@mixin ratio($keyword: false, $ratio: 16 / 9)
```

```scss|css
@include ratio(embed, 4/3);

---

display: block;
height: 0;
padding-top: 75%;
```

```scss|css
@include ratio(embed, 4/3);

---

overflow: hidden;
position: relative;
&:before {
    content: '';
    display: block;
    height: 0;
    padding-top: 75%
}
```

## resizable

```scss
@mixin resizable($value: both)
```

```scss|css
@include resizable();

---

overflow: hidden;
resize: both;
```

```scss|css
@include resizable(vertical);

---

overflow: hidden;
resize: vertical;
```

## rounded

```scss
@mixin rounded($keyword: '', $value: $defaultRadius)
```

```scss|css
@include rounded(5px);

---

border-radius: 5px;
```

```scss|css
@include rounded(top, 4px);

---

border-top-left-radius: 4px;
border-top-right-radius: 4px;
```

```scss|css
@include rounded(left, 2px);

---

border-top-left-radius: 2px;
border-bottom-left-radius: 2px;
```

## row

```scss
@mixin row($margin: $gridMargin)
```

```scss|css
@include row();

---

margin-left: -5%;
max-width: 105%;
&:after {
    clear: both;
    content: '';
    display: block;
}
```

```scss|css
@include row(10%);

---

margin-left: -10%;
max-width: 110%;
&:after {
    clear: both;
    content: '';
    display: block;
}
```
## rowModify

```scss
@mixin rowModify($margin: $gridMargin)
```

```scss|css
@include rowModify(4%);

---

margin-left: -4%;
max-width: 104%;
```

## rowReset

```scss|css
@include rowReset();

---

margin-left: 0;
max-width: none;
```

## selection

```scss
@mixin selection($color: $selectionColor, $background: $selectionBackground)
```

```scss|css
@include selection();

---

&::selection {
    background: #349bb9;
    color: #fff;
    text-shadow: none
}
```

```scss|css
@include selection(#000, #fff);

---

&::selection {
    background: #fff;
    color: #000;
    text-shadow: none
}
```

## size

```scss
@mixin size($width, $height: false)
```

```scss|css
@include size(4rem);

---

width: 4rem;
height: 4rem;
size(4rem, 250px);
width: 4rem;
height: 250px;
```


## spacedBlock

```scss
@mixin spacedBlock($margin: $blockMarginBottom, $width: false, $height: false)
```

```scss|css
@include spacedBlock($margin-bottom: 4);

---

display: block;
margin-bottom: 4rem;
```

```scss|css
@includes spacedBlock(4rem, 20rem, 100px);

---

display: block;
margin-bottom: 4rem;
width: 20rem;
height: 100px;
```

## suffix

```scss
@mixin suffix($value: '-', $margin: .5em, $font: false, $color: false)
```

```scss|css
@include suffix();

---

&:before {
    content: '-';
    margin-left: .5em;
}
```

```scss|css
@include suffix('~', 1em, $color: blue);

---

&:before {
    content: '~';
    margin-left: em;
    color: blue;
}
```


## textSharpen

```scss|css
@mixin textSharpen()

---

-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
```


## triangle

```scss
@mixin triangle($keyword, $color: $darkGray, $size: 5px, $width: $size)
```

```scss|css
@include triangle(up);

---

content: '';
height: 0;
width: 0;
border-left: 5px solid transparent;
border-right: 5px solid transparent;
border-bottom: 5px solid #737373;
```

```scss|css
@include triangle(right, $color: blue, $size: 3px);

---

content: '';
height: 0;
width: 0;
border-top: 3px solid transparent;
border-bottom: 3px solid transparent;
border-left: 3px solid blue;
```

```scss|css
@include triangle(left, red, $width: 10px);

---

content: '';
height: 0;
width: 0;
border-top: 10px solid transparent;
border-bottom: 10px solid transparent;
border-right: 5px solid red;
```