# Style guide for CSS, Sass/SCSS

## 0. Intro

Rules are provided for usage with `stylelint` npm package.

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

2. Every rule described here is aimed at time saving and ease of starting with project, its development even after long time, adding new functionality, cooperation with other memebers of team,understanding of developer intentions and fixing bugs. Since now, this reason of adding a new rule will be ommited as obvious in "Why?" sections.

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

1. Structure of stylesheet file

    * Empty files are not allowed - rule: `"no-empty-source": true`

        > Why?  
        > Empty files should be removed from repo to be not misleading for future development and don't litter project. This rule doesn't apply to starter packs.

    * First line of stylesheet cannot be empty - rule: `"no-empty-first-line": true`
    * Empty new line must be added at the end of file - rule: `"no-missing-end-of-source-newline": true`
    * Only one adjacent empty line is allowed - rule: `"max-empty-lines": 1`
    * Indentation equals to 4 spaces - rule: `"indentation": 4`

        > Why? 
        > Stylesheet should concise but visually divided into parts vertically and horizontally.

    * Max line lenght equals to 80 signs - rule: `"max-line-length": 80`
    * No whitespace at the end of line is allowed - rule: `"no-eol-whitespace": true`

        > Why?  
        > Shorter line length allows to open two stylesheets side by side on screen without scroll or moving some part of code into the next line.

2. Stylesheet settings

    * Linebreaks are expected to be LF (\n) - rule: `"linebreaks": "unix"`
    * Unicode Byte Order Mark is not allowed in stylesheet - rule: `"unicode-bom": "never"`

        > Why?  
        > **TODO**

3. **Move to declaration rule part** Only required semicolons are allowed - rule: `"no-extra-semicolons": true`

    ```css
    DO
    .class-name {
        font-size: 16px;
    }

    DON'T
    .class-name {
        font-weight: 700;;
    };
    ```
