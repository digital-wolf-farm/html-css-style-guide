# Style guide for CSS, Sass/SCSS

## 0. Intro

Rules are provided for usage with `stylelint` npm package.

## 1. Overview

1. Every front-end project should be developed using [Progressive enhancement](https://en.wikipedia.org/wiki/Progressive_enhancement) strategy. HTML is responsible for content layer of web page or app, CSS is presentional layer, while JavaScript is responsible for behaviour layer. They should be separated from each other. Content layer shouldn't know anything about presence and presence about behaviour. That results in:
    * HTML templates should only import stylesheets
    * HTML templates shouldn't contain any inline styles. Style part in head section of template is forbidden, too
    * All style should be placed in stylesheets
    * Many stylesheets used for easier development should be compiled into one file, then imported in template in production environment
    * JS shouldn't add any styles. Responsible of logic layer is only to add/remove class styled in a stylesheet to/from template element as a reaction to an event

>Why?  
>* It makes project easy to develop, read and maintain - see next point.  
>* Project is consistent with separation of concerns design principle.

2. Every rule described here is aimed at time saving and ease of starting with project, its development even after long time, adding new functionality, cooperation with other memebers of team,understanding of developer intentions and fixing bugs. Since now, this reason of adding a new rule will be ommited as obvious in "Why?" sections.

3. Start a new project with considered architecture. It costs more time at start but brings much more savings of time and nerves in the future. Macro-architecture is described in section 2 of this style guide, all next sections are about micro-architecture of projects.

4. Usage of tools to handle CSS code to lint, concatenate, add vendor prefixes before sharing it from production server it a must-have nowadays.

## 2. Project structure

1. The bigger project the more files is divided.
2. In small projects dividing stylesheet into separate files could be done when reach some number of lines and is hard to navigate. Big projects starts with defined division.
3. Code could be organized with custom rules or with chosen methodology:
    * Sass 7-1
    * SMACSS (used in my projects)
    * **TODO: Add more**  
It's important to choose one before start of development and stick to it until end of project life time.

## 3. General stylesheet rules

1. Empty files are not allowed.  
    > **Why?**  
    > Empty files should be removed from repo. Empty file like unnecessary code is misleading for understaning code in the future.

    Rule: `no-empty-source: true`

2. Empty first line is not allowed as well. But empty line at the end is required.  
    > **Why?**  
    > It provides better readability.

    Rule: `no-empty-first-line: true`  
    Rule: `no-missing-end-of-source-newline: true`

3. Linebreaks are expected to be LF (\n).  
    > **Why?**  
    > To be compatible with Git repositories.

    Rule: `linebreaks: "unix"`

4. Unicode Byte Order Mark is not allowed in stylesheet.  
    > **Why?**  
    > As far, there was no need to use they in stylesheets.

    Rule: `unicode-bom: "never"`

5. No whitespace at the end of line is allowed.  
    > **Why?**  
    > Could require more efforts to fromat code after changes.  
    > Unnecessary bytes usage.

    Rule: `no-eol-whitespace: true`

6. Only required semicolons are allowed.  
    > **Why?**  
    > Code containing misleading extra characters cost more time to understand it in the future.  
    > Unnecessary bytes usage.

    Rule: `no-extra-semicolons: true`

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

7. Only one adjacent empty line is allowed.  
    > **Why?**  
    > One empty line is enough to keep optical vertical division of adjacent parts of code.

    Rule: `max-empty-lines: 1`

8. Max length of stylesheet line equals to 80 signs.  
    > **Why?**  
    > For better work with two stylesheets opened side-by-side.  
    > For better readability.

    Rule: `max-line-length: 80`

9. Indentation is equal to 4 spaces.  
    > **Why?**  
    > To be compatible with most popular indentation of JS code.  
    > For better readability.

    Rule: `indentation: 4`