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

2. Structure of stylesheet file

    * Except starter packs or presenting structure of project, there shouldn't be empty files in repository. Leaving such files could make it hard to understand project in the future - rule: `"no-empty-source": true`.
    * First line of stylesheet cannot be empty, it should be fulfilled with comments about conctent of file or imports - rule: `"no-empty-first-line": true`.
    * Stylesheet should be ended with a new line - rule: `"no-missing-end-of-source-newline": true`.
    * One adjacent empty line is enough to divide visually code into parts - rule: `"max-empty-lines": 1`.
    * I found indentation equals to 4 spaces as more readable - rule: `"indentation": 4`.
    * Styles are not expanded as JavaScript code, so 80 characters of line lenght is enough and allow to open to stylesheets next to each other on average screen without scrolling - rule: `"max-line-length": 80`
    * No whitespace at the end of line is allowed - rule: `"no-eol-whitespace": true`

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
