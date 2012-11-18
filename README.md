# Notes from my talks on HTML & CSS 


Notes and URL's from my talk at [CanvasConf](http://2012.canvasconf.co.uk/) and [Wooweb](http://www.meetup.com/wooweb/events/78507212/).

HTML, CSS and best practices learnt whilst building a large JavaScript application.

## Our Toolbox

* HTML5 & CSS3 
* [Sass](http://sass-lang.com/) as a preprocessor
* [Compass](http://compass-style.org/) CSS3 authoring framework
* [Hogan.js](http://twitter.github.com/hogan.js/) for JavaScript templating. This was developed against the mustache test suite so everything you can do in mustache you can do with Hogan. Only faster. Allso supports template inheritance (see later).
* [Modernizr](http://modernizr.com/) feature detection
* [Grunt](http://gruntjs.com/) for task based build process in JavaScript using Node
* [Jasmine](http://pivotal.github.com/jasmine/) behaviour driven testing

## Render performance

* Look to minimize browser reflow & repaint
* Watch you use of opacity
* **visibility:hidden** instead of **display:none**
* lean HTML. Remove what you don't need

## Google Chrome dev tips

Show repaint regions live. Launch chrome with the following flags:

```
Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --show-paint-rects
```

Shows a page's actual frame rate, in frames per second, when hardware acceleration is active:

```
about:flags > fps Counter [enable]
about:flags > GPU Compositing [enable]
```


A full list of current Chromium flags can be found [here](http://peter.sh/experiments/chromium-command-line-switches/).

## CSS best practices

* use sensible defaults. Reconsider if you need a full reset script. Look to use something like [Normalise](http://necolas.github.com/normalize.css/) or write your own.
* consistent descriptive naming
* flatten CSS selectors
* use existing common patterns. Look to projects like [Bootstrap](http://twitter.github.com/bootstrap/) for inspiration
* consider a pre-processor like Sass, Less or Stylus
* comment & communicate within your dev team
* agree a style and stick to it. Look at what Nicolas has written at [Idiomatic CSS](https://github.com/necolas/idiomatic-css) as a base. Just use what you feel would work for your team

## Sass

* Extract ALL colours into a separate .scss file as variables
* Abstract common font-sizes into variables in a separate .scss file
* Look for common useage patterns and abstract into custom @mixins.
* Work with small single purpose files.
* Comment like crazy! Set a common comment style and stick to it within your company / team.

```
/* ==========================================================================
   Section comment block
   ========================================================================== */

/* Sub-section comment block
   ========================================================================== */

/**
 * Short description using Doxygen-style comment format
 *
 * The first sentence of the long description starts here and continues on this
 * line for a while finally concluding here at the end of this paragraph.
 *
 * The long description is ideal for more detailed explanations and
 * documentation. It can include example HTML, URLs, or any other information
 * that is deemed necessary or useful.
 *
 * @tag This is a tag named 'tag'
 *
 * @todo This is a todo statement that describes an atomic task to be completed
 *   at a later date. It wraps after 80 characters and following lines are
 *   indented by 2 spaces.
 */

/* Basic comment */
```
* Use Sass to join all of these small single use files together. Have an app.scss file that acts as this central point.

### Sass variables

Example of using Sass variables to make theme creation easier. This example could be taken further by abstracting out the colour variables from each of the theme .scss files.

_light.scss

```
/**
 * Color Palette
 */
$black:#111;
$white:#fff;
/* Greys */
$grey1:#ccc;
$grey2:#e6e6e6;

/**
 * Column
 */
$column-background-color:$grey1;

```

_dark.scss

```
/**
 * Color Palette
 */
$black:#111;
$white:#fff;
/* Greys */
$grey1:#202224;
$grey2:#5a5d62;

/**
 * Column
 */
$column-background-color:$white;
```

_column.scss

```
/**
 * Column
 */
.column {
    position:relative;
    display:inline-block;
    width:$column-default-width;
    /* other styles */
    background-color:$column-background-color;
}

```

Create multiple stylesheets from your Sass files. Have two top level .scss files, in each file turn on or off the browser support that you require. Example could be that you just want to generate a Webkit stylesheet alongside a full web supported stylesheet.



## CSS naming 

* don’t make names hard to understand
* decide upon a naming pattern
* move away from styling generic tags & id’s
* separate behaviour hooks from styling.

```
  // Elements for selection via JS, classes start with 'js-'
	.js-modal-close
	.js-tweet
	.js-popover

 	// Behavioural classes
	.is-hidden
	.is-animating
	.is-muted
```

## The media object

Save many lines of CSS code using [the media object](http://www.stubbornella.org/content/2010/06/25/the-media-object-saves-hundreds-of-lines-of-code/), created by Nicole Sullivan.

Example of how to use the media object can be seen [here on dabblet](http://dabblet.com/gist/3653971).

### Hogan.js template inheritance

Using template inheritance can gift you much cleaner simpler templates. In hogan v3.0 upwards but not that well documented currently.


```
	<!-- base: stream_item.mustache -->
	<article class="js-stream-item {{$stream-item-classes}}{{/stream-item-classes}}">
	    <div class="js-stream-item-content">
	        {{$content}}default content{{/content}}
	    </div>
	</article>
	
	<!--  single tweet in timeline column -->
	{{#tweet}}
	    {{<stream_item}}
	        {{$stream-item-classes}}
	            js-show-detail
	        {{/stream-item-classes}}
	
	        {{$content}}
	            <!-- render a single tweet mustache -->
	        {{/content}}
	    {{/stream_item}}
	{{/tweet}}

```

## Protoyping

Protoyping ideas and concepts can be achieved easily using an [open source Node.js based framework called Inca](https://github.com/stenson/inca).

## Thanks

Any questions hit me up on Twitter [@jmwhittaker](https://twitter.com/intent/user?screen_name=jmwhittaker).











