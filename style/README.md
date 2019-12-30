# CSS, Sass style guide

## Table of content
1. Intro
2. Requirements
3. Installation
4. Style guide for CSS
5. Style guide fos Sass/SCSS

## Intro

This style guide is prepared for using with CSS linter [stylelint.io](https://stylelint.io) and its plugins. But the rules are general and could be used with other helpers or just shared with members or your team or project to develop better code.

## Requirements for project

1. Node.js (v12.13.1*) with npm (6.12.1*) installed glabally;
2. stylelint (12.0.1*);

(*) Given version is tested, older version may work but it's not guarantee.

## Installation

1. Install `stylelint` locally with command `npm install stylelint --save-dev`;
2. Add proper scripts to `package.json` file (examples shown below are for linting all `SCSS` files inside `src` directory):
  * `"stylelint": "stylelint \"src/**/*.scss\" --syntax scss"` for starting `stylelint`;
  * `"stylelint-fix": "stylelint \"src/**/*.scss\" --syntax scss --fix"` for starting `stylelint` with auto fixing for available rules - see [documentation](https://stylelint.io/user-guide/rules);
3. Copy file `.stylelintrc.json` to directory where `package.json` file is located;
4. Run command `npm run stylelint` or `npm run stylelint-fix` to get results of linting;

## Style guide for CSS

File `styleguide.md` contains subjective style guide for `SCSS`. To apply it for pure `CSS` just use rules which concern `CSS`. All additional rules are described for better readability.
File `.stylelintrc.json` is prepared for `SCSS` files. To use it with `CSS` proper instruction will be provided.

## Style guide fos Sass/SCSS

If you are working with `SCSS` files, there is no need to change anything unless you want it.