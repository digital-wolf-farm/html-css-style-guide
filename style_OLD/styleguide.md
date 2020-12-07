# Style guide for CSS, Sass/SCSS

## 1. Overview

**Macro-architecture is described in section 2 of this style guide, all next sections are about micro-architecture of projects**

4. Usage of tools to handle CSS code to lint, concatenate, add vendor prefixes before sharing it from production server is a must-have nowadays.

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

2. Structure of stylesheet file
           
    * Nesting of rulesets introduced by Sass is nice feature which save a lot of code but in practice it should be avoided as introducing non reusable classes, non modular architecture and long selectors in output CSS files. Whole nested rulesets should as well be visible on screen to avoid poor readability. It should be used only with pseudo-classes, pseudo-elements and media queries. More about nesting in another sections. As general rule should be agreed max level of nesting limited to 2 (see: examples)

        Rule: 
        ```json
        "max-nesting-depth": 2,
        ```

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

    * After choosing methodology to make structure of project. If naming convention is not set, it's worth effort to create own for e.g. id or class names.

        Rules NOT USED: 
        ```json
        "selector-id-pattern": "",  
        "selector-class-pattern": "",
        ```

4. Documenting code

    * CSS is a markup language which doesn't document itself. When taken into consideration different browser support with their quirks, all hacks to get desired effect displayed, proper documentation of code is necessary.
    * It's a good practice to start all stylesheets, when style is divided into files, with short note of content of the file.
    * Parts of file containing styles applying to different elements should also be divided by at least titles into sections.
    * All unclear code, hacks, browser support should be commented.
    * More about format and rules concerning comments in coming section.

5. Naming elements

**TODO: DEVELOP**

## 4. Structure of CSS ruleset

Declaration block wrap declarations with curly braces. No semi-colon after closing brace.  

## 5. Rulesets

1. General rules
    * Semi-colons in CSS have strict destination. They separate declarations. Semi-colon after last declaration within ruleset could be omitted but it strongly advised to put it there always. Nowhere else in any stylesheet additional semi-colon should be added.

        Rule: 
        ```json
        "no-extra-semicolons": true,
        ```


## 6. Selectors

1. General rules
    * All style concerning one element should be placed in one ruleset. It's important to not add duplicated selectors as it makes hard to find all applied properties.

        Rule: 
        ```json
        "no-duplicate-selectors": true,
        ```

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

    * There should not be added selector with lower specifity after selector whith higher specifity.

        Rule: 
        ```json
        "no-descending-specificity": true,
        ```

    * There should not be added selectors qualifying by type (exception for attributes).
        
        Rule:  
        ```json
        "selector-no-qualifying-type": [
            true,
            {
                "ignore": "attribute"
            }
        ],
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
    * There is no black- or whitelist of combinators defined. All provided by CSS are allowed.

        Rules NOT USED: 
        ```json
        "selector-combinator-allowed-list": [],
        "selector-combinator-disallowed-list": [],
        ```
    
    * There always should be single space between elements, classes, ids or combinators in selector.

        Rules: 
        ```json
        "selector-descendant-combinator-no-non-space": true,
        "selector-combinator-space-before": "always",
        "selector-combinator-space-after": "always",
        ```

        Example
        ```css
        .class-6-2-A .class-6-2-B {
            font-size: 20px;
        }

        .class-6-2-C > .class-6-2-D {
            font-size: 12px;
        }
        ```
    * There is no rules defined about nesting selectors in pure CSS.

        Rule NOT USED: 
        ```json
        "selector-nested-pattern": "",
        ```

3. Selector specifity
    * Max value of specifity is not defined. It's up to a developer to create selectors that have specifity big enough to apply style to picked element and not too big to apply modification without `!important` or creating unnecessarily specified. Specifity is limited by rules provided in next points.

        Rule NOT USED: 
        ```json
        "selector-max-specificity": "1, 1, 1",
        ```

    * Max number of universal (`*`) and ID selectors in a selector equals to 1. Universal selector lower performance of CSS, while ID selectors should be used rarely.

        Rules: 
        ```json
        "selector-max-id": 1,
        "selector-max-universal": 1,
        ```

    * Max number of of attribute selectors or pseudo-classes is limited to 2 as properly added classes to elements within modular components resolve problems with selecting desired elements.

        Rules: 
        ```json
        "selector-max-attribute": 2,
        "selector-max-pseudo-class": 2,
        ```

    * Selectors required for maintanable and scalable template shouldn't be to long. 4 elements long selectors is enough. It could contain elements listed in previous points or be builed from only type selectors or classes. 4 elements long selector means that only 3 combinators are allowed.

        Rules: 
        ```json
        "selector-max-combinators": 3,
        "selector-max-class": 4,
        "selector-max-compound-selectors": 4,
        "selector-max-type": 4,
        ```

4. Attribute selectors
    * There is no black- or whitelist of attributes' operators defined. All provided by CSS are allowed.

        Rules NOT USED: 
        ```json
        "selector-attribute-operator-allowed-list": [],
        "selector-attribute-operator-disallowed-list": [],
        ```

    * Attribute selector should be placed in square brackets without any whitespace inside them and attribute value shoud be wrpeed with quotes.

        Rules: 
        ```json
        "selector-attribute-brackets-space-inside": "never",
        "selector-attribute-operator-space-after": "never",
        "selector-attribute-operator-space-before": "never",
        "selector-attribute-quotes": "always",
        ```

        Example:
        ```css
        input[type="text"] {
            padding: 0 0.5em;
        }
        ```
    * As attribute selectors cannot be taken classes and ids names.

        Rule: 
        ```json
        "selector-attribute-name-disallowed-list": ["class", "id"],
        ```

5. Pseudo-classes and pseudo-elements
    * There is no black- or whitelist of pseudo-classes and psuedo-elements defined. All provided by CSS are allowed.

        Rules NOT USED: 
        ```json
        "selector-pseudo-class-allowed-list": [],
        "selector-pseudo-class-disallowed-list": [],
        "selector-pseudo-element-allowed-list": [],
        "selector-pseudo-element-disallowed-list": [],
        ```
    
    * When using parentheses within pseudo-class there shouldn't be whitespace inside them.

        Rule: 
        ```json
        "selector-pseudo-class-parentheses-space-inside": "never",
        ```
    
        Example:
        ```css
        input:not([type="text"] ) {
            padding: 0 0.5em;
        }
        ```
    * There should be used double colon notation for pseudo-elements.

        Rule: 
        ```json
        "selector-pseudo-element-colon-notation": "double",
        ```

        Example:
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
    * Every selector in a selector list should be added in a new line, no white space before comma and no empty lines between adjacent selectors.

        Rules: 
        ```json
        "selector-list-comma-newline-after": "always",
        "selector-list-comma-newline-before": "never-multi-line",
        "selector-list-comma-space-after": "always-single-line",
        "selector-list-comma-space-before": "never",
        "selector-max-empty-lines": 0,
        ```

        Example:
        ```css
        .class-6-6-A,
        .class-6-6-B {
            font-size: 1rem;
            font-weight: 400;
        }
        ```

## 7. Declaration blocks

1. General rules:
    * Empty block, even without comment, are not allowed.

        Rule: 
        ```json
        "block-no-empty": true,
        ```

        Example:
        ```css
        .class-7-1-1 {
            /* comment */
        }
        ```

        Example of NOT allowed styling:
        ```css
        .class-7-1-2 {}
        .class-7-1-3 { }
        ```

    * Only one declaration per line is allowed, each line ends with semicolon (directly after value) and newline (end-of-line comment followed by a newline is exception).

        Rules: 
        ```json
        "declaration-block-single-line-max-declarations": 1,
        "declaration-block-semicolon-newline-after": "always",
        "declaration-block-semicolon-newline-before": "never-multi-line",
        "declaration-block-semicolon-space-after": "always-single-line",
        "declaration-block-semicolon-space-before": "never",
        "declaration-block-trailing-semicolon": "always",
        ``` 

2. Braces:
    * Opening brace must be in the same line as selector separated with signle space. After brace newline is required.

        Rules: 
        ```json
        "block-opening-brace-newline-after": "always-multi-line",
        "block-opening-brace-newline-before": "never-single-line",
        "block-opening-brace-space-after": "always-single-line",
        "block-opening-brace-space-before": "always",
        ``` 

    * Closing brace must be placed in the newline directyly under last declaration and followed by newline.

        Rules: 
        ```json
        "block-closing-brace-empty-line-before": "never",
        "block-closing-brace-newline-after": "always",
        "block-closing-brace-newline-before": "always-multi-line",
        "block-closing-brace-space-after": "always-single-line",
        "block-closing-brace-space-before": "always-single-line",
        ```

3. Properties:
    * Duplicated properties are not allowed.

        Rule: 
        ```json
        "declaration-block-no-duplicate-properties": true,
        ```

## 8. Declarations

1. General rules
    * There is no black- or whitelist of property-unit or property-value defined. All provided by CSS are allowed.

        Rules NOT USED: 
        ```json
        "declaration-property-unit-allowed-list": {},
        "declaration-property-unit-disallowed-list": {},
        "declaration-property-value-allowed-list": {},
        "declaration-property-value-disallowed-list": {},
        ``` 

    * In general using `!important` is not allowed. When necessary to use signle space before before and no whitespace after bang is allowed.

        Rules: 
        ```json
        "declaration-no-important": true,
        "declaration-bang-space-after": "never",
        "declaration-bang-space-before": "always",
        ``` 

    * No empty line before declaration is allowed.

        Rule: 
        ```json
        "declaration-empty-line-before": "never",
        ```

2. Syntax
    * If declaration is short should be written in one line with single space only after colon. When value is too long to fit one line, then newline after property colon is required.

        Rules: 
        ```json
        "declaration-colon-newline-after": "always-multi-line",
        "declaration-colon-space-after": "always-single-line",
        "declaration-colon-space-before": "never",
        ```

## 9. Properties

1. General rules
    * There is no black- or whitelist of properties. All provided by CSS are allowed.

        Rules NOT USED: 
        ```json
        "property-allowed-list": [],
        "property-disallowed-list": [],
        ```

    * There is no pattern for custom property defined.

        Rules NOT USED: 
        ```json
        "custom-property-empty-line-before": "always",
        "custom-property-pattern": "",
        ```

2. Shorthand properties
    * Redundand values in shorthand properties are not allowed.

        Rule: 
        ```json
        "shorthand-property-no-redundant-values": true,
        ```

    * Shorthand properties cannot override longhand properties.

        Rule: 
        ```json
        "declaration-block-no-shorthand-property-overrides": true,
        ```

        Example of NOT allowed styling:
        ```css
        .class-7-2-1 {
            margin-left: 20px;
            margin: 15px;
        }
        ```
3. Longhand properties
    * There is no restriction in using longhand properties that could be combined into shorthand properties.

        Rule NOT USED: 
        ```json
        "declaration-block-no-redundant-longhand-properties": true,
        ```

        Example:
        ```css
        .class-7-2-1 {
            margin-top: 10px;
            margin-right: 15px;
            margin-bottom: 5px;
            margin-left: 15px;
            padding: 2px 3px 5px 3px;
        }
        ```

**Nesting properties in Sass is not allowed**  
**Properties order**

## 10. Values

1. List of values
    * Values list should be placed in one line or each value in a new line. Directly after each value comma. In one line list single space after comma. No empty lines between values.

        Rules: 
        ```json
        "value-list-comma-newline-after": "always-multi-line",
        "value-list-comma-newline-before": "never-multi-line",
        "value-list-comma-space-after": "always-single-line",
        "value-list-comma-space-before": "never",
        "value-list-max-empty-lines": 0,
        ```
    
2. Strings
    * Strings could not have unescaped newline.

        Rule: 
        ```json
        "string-no-newline": true,
        ```

    * Strings must be wrapped with double quotes.

        Rule: 
        ```json
        "string-quotes": "double",
        ```

3. Numbers
    * For numbers less than 1 leading zero is required.

        Rule: 
        ```json
        "number-leading-zero": "always",
        ```

    * Trailing zero is forbidden.

        Rule: 
        ```json
        "number-no-trailing-zeros": true,
        ```

    * Max number precision is 3 decimal places.

        Rule: 
        ```json
        "number-max-precision": 3,
        ```

4. Other
    * There is not specified minimum time for animations and transitions.

        Rule NOT USED: 
        ```json
        "time-min-milliseconds": 100,
        ```

## 11. Units

1. Unit black-/whitelist
    * There is do defined black-/whitelist of available units.

        Rules NOT USED: 
        ```json
        "unit-allowed-list": [],
        "unit-disallowed-list": [],
        ```

2. Value - unit pairs
    * Zero length value (em, ex, ch, vw, vh, cm, mm, in, pt, pc, px, rem, vmin, and vmax) must be written without unit.

        Rule: 
        ```json
        "length-zero-no-unit": true,
        ```

        Example:
        ```css
        .class-name {
            margin: 0;
            padding: 0 1rem;
        }
        ```

## 12. Colours

1. General rules:
    * There should be used hsl()/hsla() function to set colours in stylesheets. This is easiest way for colour to be recognized as only one variable - angle of colour circle must be known. Second way to set colour for elements is to use rgb()/rgba() function. However, this function make matching code with rendered colour a lot harder. Hex or named colours in stylesheets are not welcomed - rules:  
        `"color-named": "never"`  
        `"color-no-hex": true`.  

        rules NOT USED, as hex colours are not allowed:  
        `"color-hex-length": "long"`  
        `"color-hex-case": "lower"`  
        `"color-no-invalid-hex": true`.

2. Values:
    * Alpha values must always use the number notation - rule: `"alpha-value-notation": "number"`.
    * Degree hues must always use the number notation - rule: `"hue-degree-notation": "number"`.
    * All functions arguments must be divided with comma - rule: `"color-function-notation": "legacy"`.

        Example:
        ```css
        .class-name {
            color: hsl(25, 30%, 30%);
            opacity: 0.2;
        }
        ```

## 13. Text

1. General rules:
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
    * Comments `//...` are not allowed - rule: `"no-invalid-double-slash-comments": true`.
    * There must be whitespace inside markes of comments - rule: `"comment-whitespace-inside": "always"`.
    * There is list of disallowed words defined - rule NOT USED: `"comment-word-disallowed-list": []`.
    * There is no pattern for comment defined - rule NOT USED: `"comment-pattern": ""`.
    * There is requirement for empty line before comment defined - rule NOT USED: `"comment-empty-line-before": "always"`.

## 15. At-rules

1. General rules:
    * There is no black- or whitelist of at-rules defined. All provided by CSS are allowed - rules NOT USED:  
    `"at-rule-allowed-list": []`  
    `"at-rule-disallowed-list": []`.
    * There is no defined list of required properties for any at-rule - rule NOT USED: `"at-rule-property-required-list": []`.
    * No duplicated `@import` rules are allowed - rule: `"no-duplicate-at-import-rules": true`.

2. Schema:
    * All at-rules defined in one line or every in a new line. When defined in one line, there must be single space after each at-rule. Space before semicolon is forbidden. Newline after semicolon is required - rules:  
    `"at-rule-name-newline-after": "always-multi-line"`  
    `"at-rule-name-space-after": "always-single-line"`  
    `"at-rule-semicolon-newline-after": "always"`  
    `"at-rule-semicolon-space-before": "never"`.
    * Before at-rule, there should be an empty line. However, two the same name at-rule could be placed in subsequent line. Empty line is not necessary also after comment or when at-rule is first nested element - rule:
    ```json
        "at-rule-empty-line-before": [
            "always",
            {
                "except": [
                    "after-same-name",
                    "first-nested"
                ],
                "ignore": [
                    "after-comment",
                    "inside-block"
                ]
            }
        ]
    ```



## 16. Functions

1. General rules:
    * There is no black- or whitelist of functions. All provided by CSS are allowed - rules NOT USED:  
        `"function-allowed-list": []`  
        `"function-disallowed-list": []`.
    * No empty lines are allowed - rule: `"function-max-empty-lines": 0`.
    * There must be whitespace after function, when there is no other character (like `,`, `)`) - rule: `"function-whitespace-after": "always"`.

        Example:
        ```css
        .class-16-1 {
            transform: translate(1, 1) scale(3);
        }

        .class-16-2 {
            transform:
                translate(1, 1)
                scale(3);
        }
        ```

2. Arguments:
    * Argument could be passed in one or in multi line. For one line rule is that directyly after each argument is comma followed by space. For multiline argument after each argument is comma followed by newline. Inside parentheses of multiline function new line is required. No spaces between parentheses and arguments - rules:  
        `"function-comma-newline-after": "always-multi-line"`  
        `"function-comma-newline-before": "never-multi-line"`  
        `"function-comma-space-after": "always-single-line"`  
        `"function-comma-space-before": "never"`  
        `"function-parentheses-newline-inside": "always-multi-line"`  
        `"function-parentheses-space-inside": "never"`.

        Example:
        ```css
        .class {
            background: hsl(100, 100%, 50%);
            transform: translate(
                1,
                1
            );
            transition-timing-function: cubic-bezier(
                0.17, 0.67, 0.83, 0.67
            );
        }
        ```

    * calc() function must be valid: expression with operator surrounded by whitespaces between arguments - rules:  
        `"function-calc-no-invalid": true`  
        `"function-calc-no-unspaced-operator": true`.
    * Only standard directions are allowed in `linear-gradient()` functions like `to top`, `30deg`, `1.5rad` or lack of this argument (default `to bottom` will be used) - rule: `"function-linear-gradient-no-nonstandard-direction": true`.
    * URL passed as argument cannot be relative (must starts with `http(s)://` not `//`) and must be quoted, but there is no scheme restrictions - rules:  
        `"function-url-no-scheme-relative": true`  
        `"function-url-quotes": "always"`.  
    Rules NOT USED:  
        `"function-url-scheme-allowed-list": []`  
        `"function-url-scheme-disallowed-list": []`.

## 17. Media queries

1. General rules:
    * There is no black- or whitelist of media feature names or their combinations with values. All provided by CSS are allowed - rules NOT USED:  
        `"media-feature-name-allowed-list": []`  
        `"media-feature-name-disallowed-list": []`  
        `"media-feature-name-value-allowed-list": []`.
    * There is no custom media query names pattern defined - rule NOT USER: `"custom-media-pattern": ""`.

2. Scheme of media features:
    * No space inside parentheses - rule: `"media-feature-parentheses-space-inside": "never"`.
    * Space after NOT before colon - rules:  
        `"media-feature-colon-space-after": "always"`  
        `"media-feature-colon-space-before": "never"`.

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
        `"media-feature-range-operator-space-before": "always"`.

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
        `"media-query-list-comma-space-before": "never"`.

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
    * There is restrictions regarding naming keyframes - rule NOT USED: `"keyframes-name-pattern": ""`.

## 19. Properties order

1. There are two major ways to order CSS properties:
    * by type
    * alphabetically.  
    Third way is random order of properties. It shouldn't be used anywhere as much more consuming to understand code and predict effects.  
    Practise showed that grouping properties by type is much more effective and simplier to develop and maintain code than alphabetical order. This styleguide recommends property-type order.
2. To force using proper order of properties, there is used `stylelint` plugin `stylelint-order`. Autofixing is enabled. Ruleset inner order and properties order is defined in file `.stylelintrc.json` at the end.
3. Order within rulesets:
    * custom properties (CSS variables): `--primaryMargin: 10px 20px;`
    * dollar variables (Sass variables): `$mainColour: hsl(25, 30%, 30%);`
    * declarations: `font-weight: 400;`
    * nested rules: `p {...}`
    * media rules: `@media () {...}`
    * other
4. Order of properties (declarations point on list above) is determined by effects of given group on layout of styled page. The most important properties concern positioning and sizing elements. Next are rules affecting visual side of style like animations, backgrounds and colours. Typography and rest of properties should be at the end of declarations. Similar properties like `font-*, text-*` should be grouped together. Longhand properties eg. `margin-*, border-*` are ordered clockwise according to values of shorthand properties: `*-top, *-right, *-bottom, *-left`.
5. List of properties groups:
    * content - `content`
    * layout - `position, float, clear, z-index`
    * display - `display, transform, perpective`
    * grid-flex - `grid, flex, justify-content, align-items, order`
    * box-model - `box-sizing, width, margin, border, padding, outline, vertical-align`
    * visibility - `oberflow, clip, visibility, opacity`
    * animation-transition - `animation, transition`
    * background-shadow - `background, box-shadow`
    * colours - `color, filter`
    * typography - `font-*, text-*, word-*, list-style`
    * other - `cursor`

**Description of each group**

6. "Other" group is not listed in `.stylelintrc.json` file as library accepts unknown entries but they must be placed below known ones. As there are rarely used properties alphabetical order is required.
7. Neither groups of properties nor properties should be divided with empty lines.

## 20. Further development
**Sass specific rules: mixins, nesting, variables - decide where to set**
