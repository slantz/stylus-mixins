# stylus-mixins

**Stylus CSS compile engine mixins**
The idea of creating these mixins has appeared with a necessity to use unified, non-spagetti code blocks.
The difference from other mixins is that's not hardcoded prefixes for each property. For instance these mixins give a user an opportunity to decide which prefixes will be included in css property block and which will be skipped.

# Rem mixin
I prefer to develop sites using rem values instead of pixels for browser to calculate dimensions on it's own. Or it's the best solution to make mobile layout for sites or apps without need to test on devices. Because the _px_ value on mobile devices with different dpi will show the virtual pixel size, but the _rem_ will show the real pixels instead.

# Px-To-Rem mixin
If you don't use some global variable for compilation separate files for browsers that don't support rems to compile proper pixel fallback, then feel free to use this mixin to generate css blocks with both _px_ and _rem_ values.
Old browsers wiil use _px_ values while new ones will overwright this value this _rem_ one.
But be sure that every extra line of code is always redundant unless you are confident with computing powers of devices you are coding for. And not afraid of possible repainting overwhelmings.

# Base-Font mixin
While setting body font-size based on the initial width of a designer's mockup, the resulting layout will be absolutely independent and scaled to any screen width on its own.
Here
- ```$initial-mockup-width``` variable represents the PSD (or other format) width of the mobile mockup.
- ```$desirable-base-font``` variable represents the html base font, which you'd prefer to use for your calculations of _rem_ values.

# Prefixer mixin
This mixin will help to generate proper vendor prefixes for css properties. You should always try not to use obsolete vendors, it's always extra unnecessary code, extra file weight and some extra headache for webview rendering engine. It's real pain for heavy huge projects.