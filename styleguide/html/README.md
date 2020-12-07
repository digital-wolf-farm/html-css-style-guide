## 3. HTML style guide

1. Description

    This chapter defines style rules and formatting intended for HTML templates.

2. Stylesheets/templates settings

    * Templates should be written in HTML5 ans used as `text/html`. Remember about setting proper `doctype` at the begining of template of whole page, partial templates doesn't require it.

    ```html
    <!DOCTYPE html>
    <html lang="pl">
        <head>
            <meta charset="utf8">
            ...
        </head>
        <body>
            ...
        </body>
    </html>
    ```

    * If page will be displayed on mobile screens, setting `viewport` is required.

    ```html
    <head>
        <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    ```

    * If scaling of page is disabled for users by `viewport`, there should be other scaling like bigger font available for people with eg. low vision.

3. HTML elements

    * Semantic elements
    * Accessibility