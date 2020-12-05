### Frontend in few words

1. Core technology stack of frontend app

    * HTML - responsible for content layer of web page or app.
    * CSS - presentional layer.
    * JavaScript - responsible for behaviour layer.

2. How to develop such apps

    Every frontend project should be developed using [Progressive enhancement](https://en.wikipedia.org/wiki/Progressive_enhancement) strategy. All listed above layers should be separated from each other. Content layer shouldn't know anything about presence and presence about behaviour. That results in:
    * HTML templates import external stylesheets
    * HTML templates shouldn't contain any inline styles. Style part in head section of template is forbidden, too
    * If some part of page or app isn't a content, it definitely shouldn't be placed in template - use stylesheet instead
    * All style should be placed in stylesheets
    * Many stylesheets used for easier development should be concatenate into one, then imported before using in production environment
    * JS shouldn't add any styles. Responsibility of logic layer is only to add/remove class styled in a stylesheet to/from template element as a reaction to an event

    Why?  
    * It makes project easy to develop, read and maintain.  
    * Project is consistent with separation of concerns design principle.

3. Every rule described here is aimed at time saving and ease of starting with project, its development even after long time, adding new functionality, cooperation with other memebers of team, understanding of developer intentions and fixing bugs.

4. Always start a new project with considered architecture. It costs more time at start but brings much more savings of time and nerves in the future. I know what I'm talking about - I went through this few times. 

    **Macro-architecture is described in section 2 of this style guide, all next sections are about micro-architecture of projects**

5. Usage of tools to handle CSS code to lint, concatenate, add vendor prefixes before sharing it from production server is a must-have nowadays.