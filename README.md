# Picturefill Web Component
A Responsive Images approach that you can use today in about as many browsers as the picture element is supported.

It is a fork of <a href="http://github.com/scottjehl/picturefill">picturefill</a> by Scott Jehl, so works in a similar fashion.

**Demo URL:** [http://ericponto.github.com/picturefill-web-component/](http://ericponto.github.com/picturefill-web-component/)

**Note:** Picturefill Web Component only works in browser with support for HTML Imports, the Shadow DOM, and custom Elements. Your best bet is to turn on all the experimental features in Chrome.

## Markup pattern and explanation

Mark up your responsive images like this.

```html
	<picture-fill alt="A giant stone face at The Bayon temple in Angkor Thom, Cambodia">
		<span data-src="small.jpg"></span>
		<span data-src="medium.jpg"     data-media="(min-width: 400px)"></span>
		<span data-src="large.jpg"      data-media="(min-width: 800px)"></span>
		<span data-src="extralarge.jpg" data-media="(min-width: 1000px)"></span>

		<!-- Who needs a fallback? -->
	</picture-fill>
```

Each `span[data-src]` element’s `data-media` attribute accepts any and all CSS3 media queries—such as `min` or `max` width, or even `min-resolution` for HD (retina) displays.

### Explained...

Notes on the markup above...

* The `picture-fill` element is a custom element that extends the HTMLImageElement...so the `alt` goes right on it.
* Each `span[data-src]` element must have a `data-src` attribute specifying the image path.
* It's generally a good idea to include one source element with no `media` qualifier, so it'll apply everywhere - typically a mobile-optimized image is ideal here.
* Each `[data-src]` element can have an optional `[data-media]` attribute to make it apply in specific media settings. Both media types and queries can be used, like a native `media` attribute, but support for media _queries_ depends on the browser (unsupporting browsers fail silently).

### How the `img` is appended

In the darkest corners of the DOM...

### HD Media Queries

* The `data-media` attribute supports [compound media queries](https://developer.mozilla.org/en-US/docs/CSS/Media_queries), allowing for very specific behaviors to emerge.  For example, a `data-media="(min-width: 400px) and (min-device-pixel-ratio: 2.0)` attribute can be used to serve a higher resolution version of the source instead of a standard definition image. Note you currently also need to add the `-webkit-min-device-pixel-ratio` prefix (e.g. for iOS devices).

```html
	<picture-fill alt="A giant stone face at The Bayon temple in Angkor Thom, Cambodia">
		<span data-src="small.jpg"></span>
		<span data-src="small_x2.jpg"      data-media="(min-device-pixel-ratio: 2.0)"></span>
		<span data-src="medium.jpg"        data-media="(min-width: 400px)"></span>
		<span data-src="medium_x2.jpg"     data-media="(min-width: 400px) and (min-device-pixel-ratio: 2.0)"></span>
		<span data-src="large.jpg"         data-media="(min-width: 800px)"></span>
		<span data-src="large_x2.jpg"      data-media="(min-width: 800px) and (min-device-pixel-ratio: 2.0)"></span>
		<span data-src="extralarge.jpg"    data-media="(min-width: 1000px)"></span>
		<span data-src="extralarge_x2.jpg" data-media="(min-width: 1000px) and (min-device-pixel-ratio: 2.0)"></span>
	</picture-fill>
```

### Supporting IE Desktop

Yeah...nope. Sorry.

### Deferred loading

The picturefill web component loads an image when the window resizes, or on the `createdCallback` method when the `picture-fill` element is created in the DOM.

## Support

Probably just Chrome/Chrome Canary with HTML imports and experimental web platform features turned on.

