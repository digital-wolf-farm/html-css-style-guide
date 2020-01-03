# Style guide for CSS, Sass/SCSS

## 0. Intro

Rules are provided for usage with `stylelint` npm package.
File `.stylelintrc.json` contains rules in the same order as described in this style guide.

## 1. Overview

1. Every front-end project should be developed using [Progressive enhancement](https://en.wikipedia.org/wiki/Progressive_enhancement) strategy. HTML is responsible for content layer of web page or app, CSS is presentional layer, while JavaScript is responsible for behaviour layer. They should be separated from each other. Content layer shouldn't know anything about presence and presence about behaviour. That results in:
    * HTML templates import external stylesheets
    * HTML templates shouldn't contain any inline styles. Style part in head section of template is forbidden, too
    * If some part of page or app isn't a content, it definitely shouldn't be placed in template - use stylesheet instead
    * All style should be placed in stylesheets
    * Many stylesheets used for easier development should be concatenate into one, then imported before using in production environment
    * JS shouldn't add any styles. Responsibility of logic layer is only to add/remove class styled in a stylesheet to/from template element as a reaction to an event

    >Why?  
    >* It makes project easy to develop, read and maintain - see next point.  
    >* Project is consistent with separation of concerns design principle.

2. Every rule described here is aimed at time saving and ease of starting with project, its development even after long time, adding new functionality, cooperation with other memebers of team,understanding of developer intentions and fixing bugs. Since now, this reason of adding a new rule will be ommited as obvious.

3. Start a new project with considered architecture. It costs more time at start but brings much more savings of time and nerves in the future. Macro-architecture is described in section 2 of this style guide, all next sections are about micro-architecture of projects.

4. Usage of tools to handle CSS code to lint, concatenate, add vendor prefixes before sharing it from production server it a must-have nowadays.

5. Every book I've read about CSS mentions that using CSS as long as it possible is better than using preprocessors like Sass. In tiny projects it makes sense. However, partials, mixins, functions, build-in minification of code and more are too big advantage to not use Sass with SCSS syntax. I prefer Sass even in not so big projects. 

## 2. Project structure

1. The bigger project the more files is divided.
2. In small projects dividing stylesheet into separate files could be done when reach some number of lines and is hard to navigate. Big projects starts with defined division.
3. Code could be organized with custom rules or with chosen methodology:
    * Sass 7-1
    * SMACSS (used in my projects)
    * **TODO: Add more**  
It's important to choose one before start of development and stick to it until end of project life time.

## 3. General stylesheet rules

1. Stylesheet settings:
    * Unicode Byte Order Mark should not be added in stylesheet as CSS files are read as UTF-8 by default by browsers - rule: `"unicode-bom": "never"`.
    * Depending on system which developer is working on different version of line-ending should be set. For Linux and macOS it's LF, while for Windows it's CRLF - rule: `"linebreaks": "windows"`.

**All rule concerning case of names**

2. Structure of stylesheet file

    * Except starter packs or presenting structure of project, there shouldn't be empty files in repository. Leaving such files could make it hard to understand project in the future - rule: `"no-empty-source": true`.
    * First line of stylesheet cannot be empty, it should be fulfilled with comments about conctent of file or imports - rule: `"no-empty-first-line": true`.
    * Stylesheet should be ended with a new line - rule: `"no-missing-end-of-source-newline": true`.
    * One adjacent empty line is enough to divide visually code into parts - rule: `"max-empty-lines": 1`.
    * I found indentation equals to 4 spaces as more readable - rule: `"indentation": 4`.
    * Styles are not expanded as JavaScript code, so 80 characters of line lenght is enough and allow to open to stylesheets next to each other on average screen without scrolling - rule: `"max-line-length": 80`
    * No whitespace at the end of line is allowed - rule: `"no-eol-whitespace": true`

**max-nesting-depth**  
**Commenting files, tables of content**

## 4. Structure of CSS ruleset

Before moving further with this style guide, small stop for theory to get clear information about presented rules.

Example of CSS ruleset:
```css
p {
    color: #fef;
    font-size: 16px;
}
```

`p` - selector  
`{ ... }` - declaration block  
`color: #fef;` - declaration  
`font-size` - property  
`16px` - property value or just value

Declaration block could concern selector or selectors list. When there is more than one selector in ruleset, they are separated by comma.  
Declaration block wrap declarations with curly braces. No semi-colon after closing brace.  
Declarations are separated by semi-colons. Last one is optional but suggested to be added.  
Colon separates property and its value.

## 5. Rulesets

no-extra-semicolons
rule-empty-line-before

## 6. Selectors

selector-pseudo-class-no-unknown
selector-pseudo-element-no-unknown
selector-type-no-unknown
no-descending-specificity
no-duplicate-selectors
selector-attribute-operator-blacklist
selector-attribute-operator-whitelist
selector-class-pattern
selector-combinator-blacklist
selector-combinator-whitelist
selector-id-pattern
selector-max-attribute
selector-max-class
selector-max-combinators
selector-max-compound-selectors
selector-max-empty-lines
selector-max-id
selector-max-pseudo-class
selector-max-specificity
selector-max-type
selector-max-universal
selector-nested-pattern
selector-no-qualifying-type
selector-no-vendor-prefix
selector-pseudo-class-blacklist
selector-pseudo-class-whitelist
selector-pseudo-element-blacklist
selector-pseudo-element-whitelist
selector-attribute-brackets-space-inside
selector-attribute-operator-space-after
selector-attribute-operator-space-before
selector-attribute-quotes
selector-combinator-space-after
selector-combinator-space-before
selector-descendant-combinator-no-non-space
selector-pseudo-class-case
selector-pseudo-class-parentheses-space-inside
selector-pseudo-element-case
selector-pseudo-element-colon-notation
selector-type-case
selector-list-comma-newline-after
selector-list-comma-newline-before
selector-list-comma-space-after
selector-list-comma-space-before

## 7. Declaration blocks

declaration-block-no-duplicate-properties
declaration-block-no-shorthand-property-overrides
block-no-empty
declaration-block-single-line-max-declarations
declaration-block-semicolon-newline-after
declaration-block-semicolon-newline-before
declaration-block-semicolon-space-after
declaration-block-semicolon-space-before
declaration-block-trailing-semicolon
block-closing-brace-empty-line-before
block-closing-brace-newline-after
block-closing-brace-newline-before
block-closing-brace-space-after
block-closing-brace-space-before
block-opening-brace-newline-after
block-opening-brace-newline-before
block-opening-brace-space-after
block-opening-brace-space-before

## 8. Declarations

declaration-block-no-redundant-longhand-properties
declaration-no-important
declaration-property-unit-blacklist
declaration-property-unit-whitelist
declaration-property-value-blacklist
declaration-property-value-whitelist
declaration-bang-space-after
declaration-bang-space-before
declaration-colon-newline-after
declaration-colon-space-after
declaration-colon-space-before
declaration-empty-line-before

## 9. Properties

property-no-unknown
shorthand-property-no-redundant-values
custom-property-pattern
property-blacklist
property-whitelist
property-no-vendor-prefix
custom-property-empty-line-before
property-case

**Properties order**

## 10. Values

string-no-newline
number-max-precision
time-min-milliseconds
value-no-vendor-prefix
number-leading-zero
number-no-trailing-zeros
string-quotes
value-keyword-case
value-list-comma-newline-after
value-list-comma-newline-before
value-list-comma-space-after
value-list-comma-space-before
value-list-max-empty-lines

## 11. Units

unit-no-unknown
unit-blacklist
unit-whitelist
length-zero-no-unit
unit-case

## 12. Colour

color-no-invalid-hex
color-named
color-no-hex
color-hex-case
color-hex-length

## 13. Text

font-family-no-duplicate-names
font-family-no-missing-generic-family-keyword
font-family-name-quotes
font-weight-notation

## 14. Comments

comment-no-empty
no-invalid-double-slash-comments
comment-word-blacklist
comment-empty-line-before
comment-whitespace-inside

## 15. At-rules

at-rule-no-unknown
no-duplicate-at-import-rules
at-rule-blacklist
at-rule-whitelist
at-rule-no-vendor-prefix
at-rule-property-requirelist
at-rule-empty-line-before
at-rule-name-case
at-rule-name-newline-after
at-rule-name-space-after
at-rule-semicolon-newline-after
at-rule-semicolon-space-before

## 16. Functions

function-calc-no-invalid
function-calc-no-unspaced-operator
function-linear-gradient-no-nonstandard-direction
function-blacklist
function-whitelist
function-url-no-scheme-relative
function-url-scheme-blacklist
function-url-scheme-whitelist
function-comma-newline-after
function-comma-newline-before
function-comma-space-after
function-comma-space-before
function-max-empty-lines
function-name-case
function-parentheses-newline-inside
function-parentheses-space-inside
function-url-quotes
function-whitespace-after

## 17. Media queries

media-feature-name-no-unknown
media-feature-name-blacklist
media-feature-name-whitelist
media-feature-name-no-vendor-prefix
media-feature-name-value-whitelist
custom-media-pattern
media-feature-colon-space-after
media-feature-colon-space-before
media-feature-name-case
media-feature-parentheses-space-inside
media-feature-range-operator-space-after
media-feature-range-operator-space-before
media-query-list-comma-newline-after
media-query-list-comma-newline-before
media-query-list-comma-space-after
media-query-list-comma-space-before

## 18. Animations

keyframe-declaration-no-important
keyframes-name-pattern
no-unknown-animations

**Sass specific rules - decide where to set**