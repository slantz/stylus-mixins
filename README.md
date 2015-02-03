# stylus-mixins

**Stylus CSS compile engine mixins**

The idea of creating these mixins has appeared with a necessity to use unified, non-spagetti code blocks.

The difference from other mixins is that's not hardcoded prefixes for each property. For instance these mixins give a user an opportunity to decide which prefixes will be included in css property block and which will be skipped.

### Rem mixin
I prefer to develop sites using rem values instead of pixels for browser to calculate dimensions on it's own. Or it's the best solution to make mobile layout for sites or apps without need to test on devices. Because the ```px``` value on mobile devices with different dpi will show the virtual pixel size, but the ```rem``` will show the real pixels instead.

You can pass:
1. one argument;
2. or arbitrary number of arguments where zero values will be left untouched;
3. additional key words
4. other built-in or arbitrary mixins;
5. special words like auto;

Let the basic ```$font-size``` be 10px

##### Mixin sample:
    1. rem(left,1)
    2. rem(padding,10 5 12 0)
    3. rem(border,1,solid green)
    4. rem(box-shadow,1 1 0 -1,rgba(0,0,0,0.3))
    5. rem(margin,10 auto 3)

##### Compiled sample:
    1. left: 0.1rem;
    2. padding: 1rem 0.5rem 1.2rem 0;
    3. border: 0.1rem solid #008000;
    4. box-shadow: 0.1rem 0.1rem 0 -0.1rem rgba(0,0,0,0.3);
    5. margin: 1rem auto 0.3rem;

### Px-To-Rem mixin
If you don't use some global variable for compilation separate files for browsers that don't support rems to compile proper pixel fallback, then feel free to use this mixin to generate css blocks with both ```px``` and ```rem``` values.

Old browsers wiil use ```px``` values while new ones will overwright this value this ```rem``` one.

But be sure that every extra line of code is always redundant unless you are confident with computing powers of devices you are coding for. And not afraid of possible repainting overwhelmings.

### Base-Font mixin
While setting body font-size based on the initial width of a designer's mockup, the resulting layout will be absolutely independent and scaled to any screen width on its own. Here

- ```$initial-mockup-width``` variable represents the PSD (or other format) width of the mobile mockup.
- ```$desirable-base-font``` variable represents the html base font, which you'd prefer to use for your calculations of ```rem``` values.

### Prefixer mixin
This mixin will help to generate proper vendor prefixes for css properties. You should always try not to use obsolete vendors, it's always extra unnecessary code, extra file weight and some extra headache for webview rendering engine. It's real pain for heavy huge projects.