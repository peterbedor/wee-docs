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
