# Style guide for CSS, Sass/SCSS
### Rules are provided by stylelint npm package

## 1. General stylesheet rules

1. Empty files are not allowed.

    Rule: `no-empty-source: true`

2. Empty first line is not allowed as well. But empty line at the end is required.

    Rule: `no-empty-first-line: true`

    Rule: `no-missing-end-of-source-newline: true`

3. Linebreaks are expected to be LF (\n).

    Rule: `linebreaks: "unix"`

4. Unicode Byte Order Mark existence in stylesheet is not defined.

    Rule not added: `unicode-bom: "never"`

5. No whitespace at the end of line is allowed.

    Rule: `no-eol-whitespace: true`

6. Only required semicolons are allowed.

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

    Rule: `max-empty-lines: 1`

8. Max length of stylesheet line equals to 80 signs.

    Rule: `max-line-length: 80`

9. Indentation is equal to 4 spaces.

    Rule: `indentation: 4`