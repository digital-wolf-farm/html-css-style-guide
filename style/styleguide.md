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
It's important to choose one before start of development and stick to it until end of project life time.

**TODO: Add more methodologies and develop this section**

## 3. General stylesheet rules

1. Stylesheet settings:
    * Unicode Byte Order Mark should not be added in stylesheet as CSS files are read as UTF-8 by default by browsers - rule: `"unicode-bom": "never"`.
    * Depending on system which developer is working on different version of line-ending should be set. For Linux and macOS it's LF, while for Windows it's CRLF - rule: `"linebreaks": "windows"`.

2. Structure of stylesheet file

    * Except starter packs or presenting structure of project, there shouldn't be empty files in repository. Leaving such files could make it hard to understand project in the future - rule: `"no-empty-source": true`.
    * First line of stylesheet cannot be empty, it should be fulfilled with comments about conctent of file or imports - rule: `"no-empty-first-line": true`.
    * Stylesheet should be ended with a new line - rule: `"no-missing-end-of-source-newline": true`.
    * One adjacent empty line is enough to divide visually code into parts - rule: `"max-empty-lines": 1`.
    * I found indentation equals to 4 spaces as more readable - rule: `"indentation": 4`.
    * Styles are not expanded as JavaScript code, so 80 characters of line lenght is enough and allow to open to stylesheets next to each other on average screen without scrolling - rule: `"max-line-length": 80`.
    * No whitespace at the end of line is allowed - rule: `"no-eol-whitespace": true`.
    * Nesting of rulesets introduced by Sass is nice feature which save a lot of code but in practice it should be avoided as introducing non reusable classes, non modular architecture and long selectors in output CSS files. Whole nested rulesets should as well be visible on screen to avoid poor readability. It should be used only with pseudo-classes, pseudo-elements and media queries. More about nesting in another sections. As general rule should be agreed max level of nesting limited to 2 (see: examples) - rule: `"max-nesting-depth": 2`.

        Example of nesting rulesets:
        ```css
        .class-1 {
            .class-2 { <- 1st level of nesting
                p { <- 2nd level of nesting
                    color: #fef;
                    font-size: 16px;
                }
            }
        }

        .class-3 {
            @media screen and (min-width: 1024px) { <- 1st level of nesting
                p { <- 2nd level of nesting
                    color: #fef;
                    font-size: 16px;
                }
            }
        }

        @media screen and (min-width: 1024px) { <- ignored media query at root level
            .class-4 {
                p { <- 1st level of nesting
                    color: #fef;
                    font-size: 16px;
                }
            }
        }
        ```

3. Writing code

    * All names should be written in lowercase with hyphens (except selectors in BEM methodology) - rules:  
        `"at-rule-name-case": "lower"`    
        `"function-name-case": "lower"`  
        `"media-feature-name-case": "lower"`  
        `"property-case": "lower"`  
        `"selector-pseudo-class-case": "lower"`  
        `"selector-pseudo-element-case": "lower"`  
        `"selector-type-case": "lower"`  
        `"unit-case": "lower"`  
        `"value-keyword-case": "lower"`.
    * It's important to check spelling errors in names used in stylesheets. While class or id names requires checking by developer manually, usage of valid and known type selectors, units, properties, etc. could be check by tools. Using known structures, names makes code easy to understand. All other things should be commented - see: `4. Documenting code` - rules:  
        `"at-rule-no-unknown": true`  
        `"media-feature-name-no-unknown": true`  
        `"no-unknown-animations": true`  
        `"property-no-unknown": true`  
        `"selector-pseudo-class-no-unknown": true`  
        `"selector-pseudo-element-no-unknown": true`  
        `"selector-type-no-unknown": true`  
        `"unit-no-unknown": true`.
    * Code written by developer shouldn't contain any vendor prefixes. As they are no longer recommended by W3C for new features and browsers dynamically changes it usage, adding prefixes should be reffered to automatic tools which base on updated database of support of available features - rules:  
        `"at-rule-no-vendor-prefix": true`  
        `"media-feature-name-no-vendor-prefix": true`  
        `"property-no-vendor-prefix": true`  
        `"selector-no-vendor-prefix": true`  
        `"value-no-vendor-prefix": true`
    * After choosing methodology to make structure of project. If naming convention is not set, it's worth effort to create own for e.g. id or class names - rules NOT USED:  
        `"selector-id-pattern": string|regex`  
        `"selector-class-pattern": string|regex` 

4. Documenting code

    * CSS is a markup language which doesn't document itself. When taken into consideration different browser support with their quirks, all hacks to get desired effect displayed, proper documentation of code is necessary.
    * It's a good practice to start all stylesheets, when style is divided into files, with short note of content of the file.
    * Parts of file containing styles applying to different elements should also be divided by at least titles into sections.
    * All unclear code, hacks, browser support should be commented.
    * More about format and rules concerning comments in coming section.

5. Naming elements

**TODO: DEVELOP**

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
Declarations are separated by semi-colons.  
Colon separates property and its value.

## 5. Rulesets

1. General rules
    * Semi-colons in CSS have strict destination. They separate declarations. Semi-colon after last declaration within ruleset could be omitted but it strongly advised to put it there always. Nowhere else in any stylesheet additional semi-colon should be added - rule: `"no-extra-semicolons": true`.
    * Between adjacent rulsets, there should be always an empty line. Exeption is first nested ruleset and ruleset after comment where there shouldn't empty line - rule: 
        ```json
        "rule-empty-line-before": [
            "always-multi-line",
            {
                "except": [
                    "first-nested"
                ],
                "ignore": [
                    "after-comment"
                ]
            }
        ]
        ```
        Example
        ```css
        //  A comment concerning ruleset
        .class-5-1-C {
            color: hsl(240, 100%, 50%);
            font-size: 24px;
        }

        .class-5-1-D {
            .class-5-1-E {
                color: hsl(120, 100%, 50%);
                font-size: 24px;
            }

            .class-5-1-F {
                color: hsl(12, 100%, 50%);
                font-size: 24px;
            }
        }
        ```


## 6. Selectors

1. General rules
    * All style concerning one element should be placed in one ruleset. It's important to not add duplicated selectors as it makes hard to find all apllied properties - rule: `"no-duplicate-selectors": true`. 

        Example of allowed styling
        ```css
        .class-6-1-A,
        .class-6-1-B {
            font-size: 14px;
        }

        .class-6-1-A {
            color: hsl(24, 100%, 50%);
        }
        ```

        Example of NOT allowed styling
        ```css
        .class-6-1-A {
            font-size: 12px;
        }

        .class-6-1-B {
            font-size: 14px;
        }

        .class-6-1-A {
            color: hsl(24, 100%, 50%);
        }
        ```
    * There should not be added selector with lower specifity after selector whith higher specifity - rule: `"no-descending-specificity": true`.
    * There should not be added selectors qualifying by type (exception for attributes) - rule:  
        ```json
        "selector-no-qualifying-type": [
            true,
            {
                "ignore": "attribute"
            }
        ]
        ```

        Example of NOT allowed styling
        ```css
        p.class-6-1-C {
            font-size: 12px;
        }

        a#class-6-1-D {
            font-size: 14px;
        }
        ```

        Allowed exception
        ```css
        input[type="text"] {
            color: hsl(24, 100%, 50%);
        }
        ```
    
2. Selector combinators (e.g. `+`, `>`)
    * There is no black- or whitelist of combinators defined. All provided by CSS are allowed - rules NOT USED:  
    `"selector-combinator-allowed-list": []`  
    `"selector-combinator-disallowed-list": []`
    * There always should be single space between elements, classes, ids or combinators in selector - rules:  
    `"selector-descendant-combinator-no-non-space": true`  
    `"selector-combinator-space-before": "always"`  
    `"selector-combinator-space-after": "always"`.

        Example
        ```css
        .class-6-2-A .class-6-2-B {
            font-size: 20px;
        }

        .class-6-2-C > .class-6-2-D {
            font-size: 12px;
        }
        ```

3. Selector specifity
    * Max value of specifity is not defined. It's up to a developer to create selectors that have specifity big enough to apply style to picked element and not too big to apply modification without `!important` or creating unnecessarily specified. Specifity is limited by rules provided in next points - rule NOT USED: `"selector-max-specificity": "1, 1, 1"`.
    * Max number of universal (`*`) and ID selectors in a selector equals to 1. Universal selector lower performance of CSS, while ID selectors should be used rarely - rules:  
    `"selector-max-id": 1`  
    `"selector-max-universal": 1`.
    * Max number of of attribute selectors or pseudo-classes is limited to 2 as properly added classes to elements within modular components resolve problems with selecting desired elements - rules:  
    `"selector-max-attribute": 2`  
    `"selector-max-pseudo-class": 2`.
    * Selectors required for maintanable and scalable template shouldn't be to long. 4 elements long selectors is enough. It could contain elements listed in previous points or be builed from only type selectors or classes. 4 elements long selector means that only 3 combinators are allowed - rules:  
    `"selector-max-combinators": 3`  
    `"selector-max-class": 4`  
    `"selector-max-compound-selectors": 4`  
    `"selector-max-type": 4`

4. Attribute selectors
    * There is no black- or whitelist of attributes' operators defined. All provided by CSS are allowed - rules NOT USED:  
    `"selector-attribute-operator-allowed-list": []`  
    `"selector-attribute-operator-disallowed-list": []`.
    * Attribute selector should be placed in square brackets without any whitespace inside them and attribute value shoud be wrpeed with quotes - rules:
    `"selector-attribute-brackets-space-inside": "never"`  
    `"selector-attribute-operator-space-after": "never"`  
    `"selector-attribute-operator-space-before": "never"`  
    `"selector-attribute-quotes": "always"`.

        Example
        ```css
        input[type="text"] {
            padding: 0 0.5em;
        }
        ```
    * As attribute selectors cannot be taken classes and ids names - rule `"selector-attribute-name-disallowed-list": ["class", "id"]`.

5. Pseudo-classes and pseudo-elements
    * There is no black- or whitelist of pseudo-classes and psuedo-elements defined. All provided by CSS are allowed - rules NOT USED:  
    `"selector-pseudo-class-allowed-list": []`  
    `"selector-pseudo-class-disallowed-list": []`  
    `"selector-pseudo-element-allowed-list": []`  
    `"selector-pseudo-element-disallowed-list": []`.
    * When using parentheses within pseudo-class there shouldn't be whitespace inside them - rule: `"selector-pseudo-class-parentheses-space-inside": "never"`.
    
        Example
        ```css
        input:not([type="text"] ) {
            padding: 0 0.5em;
        }
        ```
    * There should be used double colon notation for pseudo-elements - rule: `"selector-pseudo-element-colon-notation": "double"`.

        Example
        ```css
        button:hover {
            backgroun-color: hsl(24, 100%, 50%);
        }

        p::first-letter {
            font-size: 1.5em;
            font-weight: 700;
        }
        ```

6. Selectors lists
    * Every selector in a selector list should be added in a new line, no white space before comma and no empty lines between adjacent selectors - rules:  
    `"selector-list-comma-newline-after": "always"`  
    `"selector-list-comma-newline-before": "never-multi-line"`  
    `"selector-list-comma-space-after": "always-single-line"`  
    `"selector-list-comma-space-before": "never"`  
    `"selector-max-empty-lines": 0`

        Example
        ```css
        .class-6-6-A,
        .class-6-6-B {
            font-size: 1rem;
            font-weight: 400;
        }
        ```

## 7. Declaration blocks

1. General rules:
    * Empty block, even without comment, are not allowed - rule: `"block-no-empty": true`

        Example
        ```css
        .class-7-1-1 {
            /* comment */
        }
        ```

        Example of NOT allowed styling
        ```css
        .class-7-1-2 {}
        .class-7-1-3 { }
        ```
        
2. Properties:
    * Duplicated properties are not allowed - rule: `"declaration-block-no-duplicate-properties": true`.
    * Shorthand properties cannot override longhand properties - rule: `"declaration-block-no-shorthand-property-overrides": true`.

        Example of NOT allowed styling
        ```css
        .class-7-2-1 {
            margin-left: 20px;
            margin: 15px;
        }
        ```

declaration-block-single-line-max-declarations
declaration-block-semicolon-newline-after
declaration-block-semicolon-newline-before
declaration-block-semicolon-space-after
declaration-block-semicolon-space-before
declaration-block-trailing-semicolon
block-opening-brace-newline-after
block-opening-brace-newline-before
block-opening-brace-space-after
block-opening-brace-space-before
block-closing-brace-empty-line-before
block-closing-brace-newline-after
block-closing-brace-newline-before
block-closing-brace-space-after
block-closing-brace-space-before

## 8. Declarations

declaration-block-no-redundant-longhand-properties
declaration-no-important
declaration-property-unit-allowed-list
declaration-property-unit-disallowed-list
declaration-property-value-allowed-list
declaration-property-value-disallowed-list
declaration-bang-space-after
declaration-bang-space-before
declaration-colon-newline-after
declaration-colon-space-after
declaration-colon-space-before
declaration-empty-line-before

## 9. Properties

shorthand-property-no-redundant-values
custom-property-pattern
property-allowed-list
property-disallowed-list
custom-property-empty-line-before

**Nesting properties in Sass is not allowed**
**Properties order**

## 10. Values

1. Strings could not have unescaped newline - rule: `"string-no-newline": true`.

number-max-precision
time-min-milliseconds
number-leading-zero
number-no-trailing-zeros
string-quotes
value-list-comma-newline-after
value-list-comma-newline-before
value-list-comma-space-after
value-list-comma-space-before
value-list-max-empty-lines

## 11. Units

1. Unit black-/whitelist
    * There is do defined black-/whitelist of available units - rules NOT USED:  
        `"unit-allowed-list": []`   
        `"unit-disallowed-list": []`. 
2. Value - unit pairs
    * Zero length value (em, ex, ch, vw, vh, cm, mm, in, pt, pc, px, rem, vmin, and vmax) must be written without unit - rule: `"length-zero-no-unit": true`.  
    
        Example:
        ```css
        .class-name {
            margin: 0;
            padding: 0 1rem;
        }
        ```

## 12. Colours

1. Coding colours
    * There should be used hsl()/hsla() function to set colours in stylesheets. This is easiest way for colour to be recognized as only one variable - angle of colour circle must be known. Second way to set colour for elements is to use rgb()/rgba() function. However, this function make matching code with rendered colour a lot harder. Hex or named colours in stylesheets are not welcomed - rules:  
        `"color-named": "never"`  
        `"color-no-hex": true`.  
    
        NOT USED rules, as hex colours are not allowed:  
        `"color-hex-length": "long"`  
        `"color-hex-case": "lower"`  
        `"color-no-invalid-hex": true`.

color-function-notation
alpha-value-notation
hue-degree-notation

## 13. Text

1. Coding fonts properties:
    * Font families that name contain white space or digit or punctuation character other than hyphen are recommended to be wrapped with quotes. Keywords like: `inherit`, `sans-serif`, `cursive` cannot be wrapped into quotes, as it change it into font family with that name. Qoutes cannot be added to vendor prefixed system fonts linke `-apple-system` or `BlinkMacSystemFont`. All other names with invalid CSS identifiers (containing `$`, `!` or `/`) must be qouted - rule: `"font-family-name-quotes": "always-where-recommended"`.
    * Value for `font-family` property has to contain generic families (e.g. serif, monospace) added at the end of list - rule: `"font-family-no-missing-generic-family-keyword": true`.
    * Stylelint provides rule to disallow adding repeated font family names - rule: `"font-family-no-duplicate-names": true`.
    * Browsers could interpate named values in different ways, so properties as `font-weight` should have numeric values instead of named - rule: `"font-weight-notation": "numeric"`.

        Example:
        ```css
        .proper-example {
            font-family: MySuperFont, "Times New Roman", Times, serif;
            font-weight: 400;
        }

        .wrong-example {
            font-family: "MySuperFont", Times New Roman, Times, Times;
            font-weight: normal;
        }
        ```

## 14. Comments

1. General rules:
    * No empty comments are allowed - rule: `"comment-no-empty": true`.
    * Comments `//...` are not allowed - rule: `"no-invalid-double-slash-comments": true`

comment-word-disallowed-list
comment-empty-line-before
comment-whitespace-inside
comment-pattern

## 15. At-rules

1. General rules:
    * No duplicated `@import` rules are allowed - rule: `"no-duplicate-at-import-rules": true`.

at-rule-disallowed-list
at-rule-allowed-list
at-rule-property-required-list
at-rule-empty-line-before
at-rule-name-newline-after
at-rule-name-space-after
at-rule-semicolon-newline-after
at-rule-semicolon-space-before

## 16. Functions

1. Functions rules:
    * calc() function must be valid: expression with operator surrounded by whitespaces between arguments - rules:
        `"function-calc-no-invalid": true`,
        `"function-calc-no-unspaced-operator": true`.
    * Only standard directions are allowed in `linear-gradient()` functions like `to top`, `30deg`, `1.5rad` or lack of this argument (default `to bottom` will be used) - rule: `"function-linear-gradient-no-nonstandard-direction": true`.


function-allowed-list
function-disallowed-list
function-url-no-scheme-relative
function-url-scheme-allowed-list
function-url-scheme-disallowed-list
function-comma-newline-after
function-comma-newline-before
function-comma-space-after
function-comma-space-before
function-max-empty-lines
function-parentheses-newline-inside
function-parentheses-space-inside
function-url-quotes
function-whitespace-after

## 17. Media queries

1. General rules:
    * There is no black- or whitelist of media feature names or their combinations with values. All provided by CSS are allowed - rules NOT USED:  
        `"media-feature-name-allowed-list": []`  
        `"media-feature-name-disallowed-list": []`
        `"media-feature-name-value-allowed-list": []`
    * There is no custom media query names pattern defined - rule NOT USER: `"custom-media-pattern": ""`
2. Scheme of media features:
    * No space inside parentheses - rule: `"media-feature-parentheses-space-inside": "never"`.
    * Space after NOT before colon - rules:
        `"media-feature-colon-space-after": "always"`
        `"media-feature-colon-space-before": "never"`

        Example:
        ```css
        @media (min-width: 1280px) {
            .class {
                font-size: 16px;
            }
        }
        ```

    * Space before and after range operators - rules:
        `"media-feature-range-operator-space-after": "always"`
        `"media-feature-range-operator-space-before": "always"`

        Example:
        ```css
        @media (width >= 1280px) {
            .class {
                width: 250px;
            }
        }
        ```

3. Media query lists:
    * Lists of media queries, if not placed in one line, should have all lines ended with comma. No space before comma, only after - rules:
        `"media-query-list-comma-newline-after": "always-multi-line"`
        `"media-query-list-comma-newline-before": "never-multi-line"`
        `"media-query-list-comma-space-after": "always-single-line"`
        `"media-query-list-comma-space-before": "never"`

        Example:
        ```css
        @media screen, printer {
            .class {
                width: 250px;
            }
        }

        @media screen,
        printer {
            .class {
                width: 250px;
            }
        }
        ```

## 18. Animations

1. General rules
    * `!important` keyword is not allowed within keyframe declarations (some browsers ignore it) - rule: `"keyframe-declaration-no-important": true`.
    * There is restrictions regarding naming keyframes - rule NOT USED: `"keyframes-name-pattern": ""`

## 19. Further development
**Sass specific rules: mixins, nesting, variables - decide where to set**

selector-nested-pattern