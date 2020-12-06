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

            Of course, path have to be adjusted to your project directory structure. Command above will lint all CSS files in all directories located in `src` directory. Second command will fix stylesheets for rules with auto fix option - see [documentation](https://stylelint.io/user-guide/rules/list).

        * If work with SCSS files (what are `*.scss` files will be explained in chapter about Sass, how to start using Sass in own project - open appendix):

            ```json
            "stylelint": "stylelint \"src/**/*.scss\" --syntax scss",
            "stylelint-fix": "stylelint \"src/**/*.scss\" --syntax scss --fix",
            ```

    * Add file `.stylelintrc.json` with rules to directory where `package.json` file is located.
    * Run command `npm run stylelint` or `npm run stylelint-fix` to get results of linting.

3. `.stylelintrc.json` explained in few words

    * All used plugins and rules for `Stylelint` are place in this file.
    * It could have other name and more options added - see [documentation](https://stylelint.io).
    * Available plugins are listed [here](https://github.com/stylelint/awesome-stylelint#plugins).
    * Documents for all rules are [here](https://stylelint.io/user-guide/rules/list).
    * This file consists of two parts - array of used plugins and object containing list of all used rules.

        ```json
        {
            "plugins": [
                "stylelint-order"
            ],
            "rules": {}
        }
        ```
    * Plugins' rules are added at the bottom of list and usually are prefixed by authors.
    * File doesn't contain all available rules. Style guide lists all used and not used rules in proper sections.
    * File could be modified freely or replaced with rules better suited to your project requirements.

4. Convention of this Style guide

    Each chapter describe different part of frontend technology stack (currently no JS Style Guide). Sections of chapters divide rules into common chunks. They are mostly ordered from outer to inner and top to bottom part of issue. Some exception may occurs intentionally or not.

    Rules consists of short description and explaination if there is any reason aside from ones listed in next section. If description is not enough to explain rule, there is example of proper and wrong code (Chapter - Common style guide presents first exmaple in HTML, latter in CSS). If `Styleguide` provides proper rules, they are listed with information if some of them are not used.
        