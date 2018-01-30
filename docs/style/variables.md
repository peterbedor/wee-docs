## Addresses

```scss
$addressColor: $darkestGray;
$addressFont: $baseFont;
$addressFontSize: $baseFontSize;
$addressFontWeight: normal;
$addressFontStyle: normal;
$addressLineHeight: $paragraphLineHeight;
```

## Base

```scss
$rootFontSize: 62.5%;

$baseColor: $darkestGray;
$baseFont: Arial, Helvetica, sans-serif;
$baseFontSize: 1.6rem;
$baseFontWeight: normal;
$baseLineHeight: 1em;

$bodyBackground: $white;
```

## Buttons

```scss
$buttonStyled: true;

$buttonColor: $white;
$buttonFont: $baseFont;
$buttonFontSize: $baseFontSize;
$buttonFontWeight: normal;

$buttonPaddingHorizontal: 3rem;
$buttonPaddingVertical: 1.3rem;

$buttonMarginBottom: false;

$buttonRounded: $defaultRadius; // false to disable

$buttonTransitionEnabled: false;
$buttonTransitionProperty: background-color;
$buttonTransitionDuration: $defaultDuration;

$buttonActiveTransitionEnabled: false;
$buttonActiveTransitionProperty: background-color;
$buttonActiveTransitionDuration: $defaultDuration;

$buttonBackground: $darkGray;
$buttonBackgroundHover: darken($buttonBackground, 5%);
$buttonBackgroundActive: darken($buttonBackground, 10%);

$buttonBorderColor: false; // false to disable

// Colored Buttons

$coloredButtonClassModifier: colored-button;

$coloredButtonColor: $white; // font color

$coloredButtonBackground: $linkColor;
$coloredButtonBackgroundHover: darken($coloredButtonBackground, 5%);
$coloredButtonBackgroundActive: darken($coloredButtonBackground, 10%);

$coloredButtonBorderColor: false;

// Disabled Buttons

$disabledButtonClassModifier: -disabled;

$disabledButtonColor: $darkGray;

$disabledButtonBackground: $lightGray;

$disabledButtonBorderColor: false;

$disabledButtonCursor: not-allowed;
```

## Code

```scss
$codeColor: $darkestGray;
$codeFont: monospace;
$codeFontSize: $baseFontSize;
$codeLineHeight: 1.4em;

$codeBackground: $lighterGray;

$codeBorderColor: false;
$codeRounded: false;

$codePaddingHorizontal: .5em;
$codePaddingVertical: .2em;

$codeBlockColor: $lightestGray;
$codeBlockFont: $codeFont;
$codeBlockFontSize: 1.3rem;
$codeBlockLineHeight: $paragraphLineHeight;
$codeBlockTabSize: 4;
$codeBlockWrap: false;
$codeBlockMarginBottom: $blockMarginBottom;

$codeBlockBackground: $darkestGray;

$codeBlockBorderColor: $codeBorderColor; // false to disable
$codeBlockRounded: false;

$codeBlockPaddingHorizontal: 2rem;
$codeBlockPaddingVertical: 1.4rem;
```

## Colors

```scss
$primary: #5789ff;
$secondary: #121212;
$tertiary: #ff9b57;
$info: #1a28ff;
$success: #2ed183;
$warning: #ff4121;
```

## Fonts

```scss
$fontPath: '../fonts/'; // absolute or relative path
$iconFont: icons;
$woff2Enabled: true; // false to disable
```

## Forms

```scss
// Inputs

$inputColor: $darkerGray;
$inputFont: $baseFont;
$inputFontSize: $baseFontSize;
$inputFontWeight: $baseFontWeight;

$inputBackground: $white;

$inputBorderColor: $lighterGray;
$inputBorderColorHover: darken($inputBorderColor, 10%);
$inputBorderColorFocus: darken($inputBorderColor, 20%);
$inputBorderWidth: 1px;        // false to disable
$inputRounded: $defaultRadius; // false to disable

$inputMinWidth: 20rem; // false to disable
$inputMinHeight: 3rem; // false to disable

$inputPaddingHorizontal: 1.6rem;
$inputPaddingVertical: 1rem;

$inputMarginBottom: 2rem;

$inputPlaceholderColor: lighten($inputColor, 40%);

// Invalid Inputs

$inputBackgroundInvalid: $white;
$inputBorderColorInvalid: #a41818;
$inputColorInvalid: darken($inputBorderColorInvalid, 10%);
$inputBorderColorInvalidHover: darken($inputBorderColorInvalid, 10%);
$inputBorderColorInvalidFocus: darken($inputBorderColorInvalid, 20%);
$inputBorderWidthInvalid: 1px; // false to disable

// Required Inputs

$inputBackgroundRequired: $white;
$inputBorderColorRequired: $darkGray;
$inputColorRequired: darken($inputBorderColorRequired, 10%);
$inputBorderColorRequiredHover: darken($inputBorderColorRequired, 10%);
$inputBorderColorRequiredFocus: darken($inputBorderColorRequired, 20%);
$inputBorderWidthRequired: 1px; // false to disable

// Disabled Inputs

$inputColorDisabled: $darkGray;

$inputBackgroundDisabled: $lightestGray;

$inputBorderWidthDisabled: false; // false to disable

$inputCursorDisabled: not-allowed;

$inputDisabledModifier: -disabled;
$inputDisabledCursor: not-allowed;

// Selects

$multiSelectMinHeight: 8rem;

// Checkboxes

$checkboxMarginBottom: 1rem;
$checkboxMarginRight: .5rem;

// Textareas

$textareaLineHeight: 1.3em;
$textareaMinHeight: 8rem;
$textareaResize: vertical; // none, horizontal, vertical, both
$textareaPaddingHorizontal: 1.6rem;
$textareaPaddingVertical: 1rem;

// Legends

$legendColor: $darkerGray;
$legendFont: $baseFont;
$legendFontSize: 1.8rem;

$legendMarginBottom: 1.4rem;

// Labels

$labelFontWeight: normal;
$labelLineHeight: 1.3em;

$labelMarginBottom: .4rem;
$labelMarginRight: 1rem;
```

## Grayscale

```scss
$white: #fff;
$lightestGray: darken(#fff, 4%);
$lighterGray: darken(#fff, 10%);
$lightGray: darken(#fff, 25%);
$gray: darken(#fff, 35%);
$darkGray: darken(#fff, 55%);
$darkerGray: darken(#fff, 65%);
$darkestGray: darken(#fff, 75%);
$black: #000;
```

## Headings

```scss
$headingColor: inherit;
$headingFont: Tahoma, Geneva, sans-serif;
$headingFontWeight: $boldFontWeight;
$headingLineHeight: 1.4em;

$headingMarginBottom: 2rem;

$h1: 3.6rem; // font sizes
$h2: 3.2rem;
$h3: 2.8rem;
$h4: 2.4rem;
$h5: 2rem;
$h6: 1.6rem;
```

## Horizontal Rule

```scss
$ruleColor: $lightGray;
$ruleHeight: 1px;
$ruleStyle: solid;
$ruleMargin: $blockMarginBottom;
```

## Images

```scss
$imagePath: '../images/'; // absolute or relative path
$spriteFilename: 'sprite.png'; // relative to image path above

$retinaSuffix: '-2x'; // retina filename suffix

$retinaSpriteWidth: auto;
$retinaSpriteHeight: auto;

// Margin applied when using img-left and img-right classes

$imageMarginBottom: 2rem;
$imageMarginSide: 2rem;

// Figures

$figureBorderColor: false; // false to disable
$figureRounded: false;

$figurePadding: $blockMarginBottom;

// Figure Captions

$figCaptionColor: $darkGray;
$figCaptionFontStyle: italic;
$figCaptionLineHeight: $paragraphLineHeight;

// Alignment

$imageLeftClass: img-left;
$imageRightClass: img-right;
```

## Layout

```scss
$minWidth: false;  // min container width, false to disable
$maxWidth: 1280px; // max container width, false to disable

$bumperPadding: 6%;  // bumper padding on containers, false to disable
$padContainer: true; // enable bumperPadding on containers

$gridMargin: 5%; // default margin for spaced columns
$gridColumns: 8; // default number of columns in grid

$gridSpaceless: false; // set to true to eliminate inline grid whitespace hack

$blockMarginBottom: 4rem; // default spacing for lists, form elements, and other blocks
```

## Links

```scss
$linkColor: $primary;
$linkColorHover: darken($linkColor, 10%);
$linkColorActive: darken($linkColor, 20%);

$linkDecoration: none;       // none, underline
$linkDecorationHover: false; // none, underline, false
```

## Miscellaneous

```scss
$smallFontSize: .8em;

$selectionColor: $white;
$selectionBackground: $linkColor;

$boldFontWeight: bold;
$normalFontWeight: normal;

$markColor: $baseColor;
$markBackground: yellow;

$defaultRadius: 3px;
$defaultOpacity: .2;
$defaultDuration: .2s;
$defaultTiming: ease-in-out;

$abbrUnderline: dotted; // dotted, solid, none
```

## Paragraphs

```scss
$paragraphColor: $baseColor;
$paragraphFontWeight: $baseFontWeight;
$paragraphLineHeight: 1.7em;

$paragraphMarginBottom: 2rem;
```

## Print

```scss
$printPageMargin: 2cm .5cm;
```

## Quotes

```scss
$quoteColor: $darkestGray;
$quoteFont: Georgia, Times, serif;
$quoteFontSize: 2rem;
$quoteFontStyle: italic;
$quoteFontWeight: normal;
$quoteLineHeight: 1.4em;

$quotePaddingHorizontal: 2em;
$quotePaddingVertical: 1em;

// Cites

$citeColor: $gray;
$citeFont: $baseFont;
$citeFontSize: 1.8rem;
$citeFontStyle: normal;
$citeFontWeight: normal;
$citeLineHeight: 1.2em;

$citeMarginTop: 1.4rem;

$citeIndicator: '\2014\00a0';
```
