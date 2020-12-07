### Rules

1. Stylesheets
    * Structure   
        Every stylesheet within project should have the same structure set before first keystroke. Starts with optional comment with description of content - more in section about comments. Then general at-rules, custom properties and finally rulesets. Every group should be separated from each other with one empty line. Additionally, every ruleset should be preceded by an empty line. Exceptions are for:
        * first ruleset in a stylesheet, where there is no other elements before. In such case stylesheet starts with ruleset in first line.
        * first nested ruleset (it applies to Sass).
        * rulesets place after comment.

        ```css
        .class1 {
            .class2 {
                color: hsl(120, 100%, 50%);
                font-size: 24px;
            }

            .class3 {
                color: hsl(12, 100%, 50%);
                font-size: 24px;
            }
        }

        /* Comment */
        .class4 {
            color: hsl(240, 100%, 50%);
            font-size: 24px;
        }
        ```

        Stylelint rule: 
        ```json
        "rule-empty-line-before": [
            "always-multi-line",
            {
                "except": [
                    "first-nested"
                ],
                "ignore": [
                    "after-comment"
                ]
            }
        ],
        ```

        <!-- Add examples -->

2. Rulesets

3. Selectors

4. Declaration blocks

5. Declarations

6. Properties

7. Values

8. Units

9. Colours

10. Text

11. Comments

12. Box-model

13. Functions

14. At-rules

15. Media queries

16. Animations

17. Other rules

    * Vendor prefixes   
        Browser support of CSS features is changing constantly. Manual maintenance of vendor prefix in stylesheets is redundant effort. There are tools like PostCSS with plugin Autoprefixer which automate such work with better results as get up-to-date database of required prefixes from repository. Thus, adding vendor prefixes to any part of stylesheets is not recommended.

        ```css
        /* Recommended */
        transition: left 1s ease-in-out 0.1s;

        /* Not recommended */
        -webkit-transition: left 1s ease-in-out 0.1s;
        transition: left 1s ease-in-out 0.1s;
        ```

        Stylelint rules: 
        ```json
        "at-rule-no-vendor-prefix": true,
        "media-feature-name-no-vendor-prefix": true,
        "property-no-vendor-prefix": true,
        "selector-no-vendor-prefix": true,
        "value-no-vendor-prefix": true,
        ```
