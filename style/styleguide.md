# Style guide for CSS, Sass/SCSS
### Rules are provided by `stylelint` npm package

## 1. General stylesheet rules

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