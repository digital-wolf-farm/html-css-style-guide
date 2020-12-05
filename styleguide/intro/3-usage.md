### How to use this style guide

1. Using this knowledge in any project:
    * First option is just read, think of possible changes and apply to your project.
    * Second option is cloning repo and playing with it - modifying rules, changing examples to match needs.
    * Another option is to install required dependencies add scripts and copy file `.stylelintrc.json`.

2. Using `Stylelint` in own project:

    * Basic requirements - `Node.js` installed globally is required and project initialized with `npm init`.
    * Install locally linter as dev dependency - `npm install --save-dev stylelint [list of plugins]`.
    * Add scripts to your `package.json` file:
        * If work with CSS:

            ```json
            "stylelint": "stylelint \"src/**/*.css\"",
            "stylelint-fix": "stylelint \"src/**/*.css\" --fix",
            ```

            Of course, path have to be adjusted to your project directory structure. Command above will lint all CSS files in all directories located in `src` directory. Second command will fix stylesheets for rules with auto fix option - see [documentation](https://stylelint.io/user-guide/rules).

        * If work with SCSS files (what are `*.scss` files will be explained in chapter about Sass):

            ```json
            "stylelint": "stylelint \"src/**/*.scss\" --syntax scss",
            "stylelint-fix": "stylelint \"src/**/*.scss\" --syntax scss --fix",
            ```

    * Add file `.stylelintrc.json` with rules to directory where `package.json` file is located.
    * Run command `npm run stylelint` or `npm run stylelint-fix` to get results of linting;