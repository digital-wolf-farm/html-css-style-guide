## 2. Common style guide

1. Description

    This chapter defines style rules and formatting common for HTML templates and CSS stylesheets.

2. Stylesheets/templates settings

    * Encoding  
        Use UTF-8 without byte order mark (BOM) in your editor. Don't add charset rule to your stylesheet as UTF-8 is default value. While add proper meta to HTML files.

        ```html
        <!-- Recommended -->
        <meta charset="utf-8">
        ```

        ```css
        /* Not recommended */
        @charset "UTF-8";
        ```

        Stylelint rule:
        ```json
        "unicode-bom": "never",
        ```

    * Line ending  
        Set one line ending for all files on all computers commiting to project. For Linux and macOS it's LF, while for Windows it's CRLF.

        Stylelint rule:
        ```json
        "linebreaks": "windows",
        ```

3. Document structure

    * Empty files  
        Do not add empty files to project until have content to fill them. If it's required for future development add proper comment inside it.

        Stylelint rule: 
        ```json
        "no-empty-source": true,
        ```

    * Lines number per file  
        For JavaScript such rule can be set, for templates and stylesheet it not so easy as it depends on content. General rule says try to keep files as short as possible. Put not related code into separated files. With project growing into enterprise scale more files are welcomed.
    
    * Line length  
        Line length equal to 80 characters is proper to be readable and allow to open two files on average screen next to each other without scrolling. This rule is more for HTML documents. More details about wrapping code - see: HTML Style Guide.

        Stylelint rule: 
        ```json
        "max-line-length": 80,
        ```

    * Indentation  
        There are as many opinions as many are developers. This style guide recommend indentation equals to 4 spaces as more readable.

        Stylelint rule: 
        ```json
        "indentation": 4,
        ```
    
    * First line  
        Do not leave empty first line. If there is no need to add comment or import at the begin, start coding from the first line.

        Stylelint rule: 
        ```json
        "no-empty-first-line": true,
        ```
    
    * Last line  
        All files should be ended with empty line.

        Stylelint rule: 
        ```json
        "no-missing-end-of-source-newline": true,
        ```

    * Empty lines between code  
        One empty line to divide code visually into sections is enough.

        Stylelint rule: 
        ```json
        "max-empty-lines": 1,
        ```

    * Trailing whitespace  
        No trailing whitespace is allowed.

        Stylelint rules: 
        ```json
        "no-eol-whitespace": true,
        ```

4. Other common rules

    * Letter case  
        All code should be written in lowercase:
        * HTML - tags, attributes, values;
        * CSS - at-rules, media features, functions, selectrors, properties, values and units.
        Exception is text content displayed on page which should meet requirements. More about naming in the following chapters.

        Stylelint rules: 
        ```json
        "at-rule-name-case": "lower",
        "function-name-case": "lower",
        "media-feature-name-case": "lower",
        "property-case": "lower",
        "selector-pseudo-class-case": "lower",
        "selector-pseudo-element-case": "lower",
        "selector-type-case": "lower",
        "unit-case": "lower",
        "value-keyword-case": "lower",
        ```
    
    * Typos  
        To code works as expected, it's important to check all typos. Unfortunately checking HTML file same as ids and classes name is manual work.

        Stylelint rules: 
        ```json
        "at-rule-no-unknown": true,
        "media-feature-name-no-unknown": true,
        "no-unknown-animations": true,
        "property-no-unknown": true,
        "selector-pseudo-class-no-unknown": true,
        "selector-pseudo-element-no-unknown": true,
        "selector-type-no-unknown": true,
        "unit-no-unknown": true,
        ```

    * Protocols  
        Do not omit protocol in urls not stored locally.

        ```html
        <!-- Recommended -->
        <script src="https://some-cdn.com/libs/lib.min.js">

        <!-- Not recommended -->
        <script src="//some-cdn.com/libs/lib.min.js">
        ```

        ```css
        /* Recommended */
        @import "https://font-cdn.com/awesome-font";

        /* Not recommended */
        @import "//font-cdn.com/awesome-font";
        ```
