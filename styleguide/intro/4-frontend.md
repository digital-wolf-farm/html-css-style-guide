### Frontend in few words

1. Layers of every frontend app:

    * content/structure layer - HTML.
    * presentional layer - CSS.
    * behaviour layer - JavaScript.

2. Reasons of dividing app into layers

    Division into layers is caused by whole variety of devices with different possibilities which can open page or web app. Content layer as the most important and basic layer should be opened and provide basic functionality on every device. It's better to show anything than nothing. Another layers should only add more possibilities of using app on more advanced devices. All layers should be separated from each other as much as possible and know about each other as little as possible. This approach is called [Progressive enhancement](https://en.wikipedia.org/wiki/Progressive_enhancement) strategy. And every frontend project should use this strategy, when there is no other strategy defined. This approach goes hand in hand with Mobile First strategy.

3. Progressive enhancement in practice

    * HTML templates import external stylesheets.
    * HTML templates shouldn't contain any inline styles. Style part in head section of template is forbidden, too.
    * If some part of page or app isn't a content, it definitely shouldn't be placed in template - use stylesheet instead.
    * All style should be placed in stylesheets.
    * Many stylesheets used for easier development should be concatenate into one, then imported before using in production environment.
    * JS shouldn't add any styles. Responsibility of logic layer is only to add/remove class styled in a stylesheet to/from template element as a reaction to an event.

    Why?  
    * It makes project easy to develop, read and maintain.  
    * Project is consistent with separation of concerns design principle.

4. In opposite to Progressive enhancement there is strategy [Graceful degradation](https://developer.mozilla.org/en-US/docs/Glossary/Graceful_degradation) where app is developed for newest browsers and most powerful devices with support for older, slower devices, where provides alternative behaviours and/or hide some content (eg. YouTube player: default is HTML5. If not accessible then uses Flash. If even Flash is not accessible then show info about lack of possibility of displaying video). This strategy does not meet requirements of accessibility.

5. More lines of code and more files in project doesn't mean lower quality. It's only indications of applying good architecture, which resolves in:

    * predictability (knowledge of responsibility of every piece of code, ease of finding part of code, knowledge where to put a new piece of code),
    * code reusing,
    * extensibility (adding new features),
    * ease of maintanance.

    This style guide aims to help archieve elements of good architecture.

6. Always start a new project with considered architecture. It costs more time at start but brings much more savings of time and nerves in the future. I know what I'm talking about - I went through this few times. 
