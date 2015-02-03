# stylus-mixins

**Stylus CSS compile engine mixins**

The idea of creating these mixins has appeared with a necessity to use unified, non-spagetti code blocks.

The difference from other mixins is that's not hardcoded prefixes for each property. For instance these mixins give a user an opportunity to decide which prefixes will be included in css property block and which will be skipped.

### Rem mixin
I prefer to develop sites using rem values instead of pixels for browser to calculate dimensions on it's own. Or it's the best solution to make mobile layout for sites or apps without need to test on devices. Because the ```px``` value on mobile devices with different dpi will show the virtual pixel size, but the ```rem``` will show the real pixels instead.

This mixin has a built-in fallback technique for old browsers. You should have some global variable set to true in order to calculate everything in pixels. Here

- ```$is-ie8``` global variable tells mixin to generate pixel values instead of ```rems```;
- ```$base-font``` global variable represents the initial divider for ```rem``` generation.

You can pass:
1. one argument;
2. or arbitrary number of arguments where zero values will be left untouched;
3. additional key words;
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

But be aware of that every extra line of code is always redundant unless you are confident with computing powers of devices you are coding for. And not afraid of possible repainting overwhelmings. Here

- ```$base-font``` global variable represents the initial divider for ```rem``` generation.

You can pass:
1. one argument;
2. or arbitrary number of arguments where zero values will be left untouched;
3. additional key words;
4. other built-in or arbitrary mixins;
5. special words like auto;

Let the basic ```$font-size``` be 10px

##### Mixin sample:
    1. rem(left,1)
    2. rem(padding,10 5 12 0)
    3. rem(border,1,solid green)
    4. rem(margin,10 auto 3)

##### Compiled sample:
    1. left: 1px;
       left: 0.1rem;
    2. padding: 10px 5px 12px 0;
       padding: 1rem 0.5rem 1.2rem 0;
    3. border: 1px solid #008000;
       border: 0.1rem solid #008000;
    4. margin: 10px auto 3px;
    4. margin: 1rem auto 0.3rem;

### Base-Font mixin
In case you need to design fully flexible and "rubber" mobile site, or some application based on HTML views, and you want to be confident about different screen sizes, then due to this technique you will have same view on any device iff your mockup is fine for sure)).

While setting body font-size based on the initial width of a designer's mockup, the resulting layout will be absolutely independent and scaled to any screen width on its own. Here

- ```$initial-mockup-width``` variable represents the PSD (or other format) width of the mobile mockup.
- ```$mdeia-divider-step``` variable represents the step of media-query iteration in order to set the ```<html>``` element's font-size to be integer.
- ```$mdeia-lowest-width``` variable represents the lowest min-width media-query if there's no need t osupport tiny screens, by default will be ```0```.
- ```$base-font``` variable represents the html base font, which you'd prefer to use for your calculations of ```rem``` values.

So if we have some mockup, e.g. designed for iPhone 5 screen, designers always draw in real device pixels, not taking into account the virtual ones, so the mockup width will be ```640px```.

Font-size for our project will be ```10px``` (it's always ease to divide by 10 inwardly). To preserve all the ratios of the mockup on any screen we will need to iterate the ```<html>``` base font-size. For instance for ```320px width screen``` the font-isze for ```<html>``` will be decreased by two, because mockup width divided by initial base-font will give us step of other divisions. And current screen width divided by this step will be ```320 / (640 / 10) = 5``` which is exactly twice less than initial base font-size.

And as ```rem``` values calculated from the root of the document => all dimensions will be lessened twice.

### Prefixer mixin
This mixin will help to generate proper vendor prefixes for css properties. You should always try not to use obsolete vendors, it's always extra unnecessary code, extra file weight and some extra headache for webview rendering engine. It's real pain for heavy huge projects.

You can pass:
1. one argument;
2. or arbitrary number of arguments;
3. exclude redundant vendors.

##### Mixin sample:
    1. prefixer(border-radius,0)
    2. prefixer(transform,unquote("rotateX(5deg) translateY(10px) skew(5deg,5deg)"))
    3. prefixer(box-sizing,border-box,-moz- -ms-)

##### Compiled sample:
    1. -webkit-border-radius: 0;
       -moz-border-radius: 0;
       -ms-border-radius: 0;
       -o-border-radius: 0;
       border-radius: 0;
    2. -webkit-transform: rotateX(5deg) translateY(10px) skew(5deg,5deg);
       -moz-transform: rotateX(5deg) translateY(10px) skew(5deg,5deg);
       -ms-transform: rotateX(5deg) translateY(10px) skew(5deg,5deg);
       -o-transform: rotateX(5deg) translateY(10px) skew(5deg,5deg);
       transform: rotateX(5deg) translateY(10px) skew(5deg,5deg);
    3. -webkit-box-sizing: border-box;
       -o-box-sizing: border-box;
       box-sizing: border-box;