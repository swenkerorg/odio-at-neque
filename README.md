# @swenkerorg/odio-at-neque.js #

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![TypeScript](https://img.shields.io/badge/%3C%2F%3E-TypeScript-%230074c1.svg)](http://www.typescriptlang.org/)
[![Socket Badge](https://socket.dev/api/badge/npm/package/@swenkerorg/odio-at-neque)](https://socket.dev/npm/package/@swenkerorg/odio-at-neque)
[![jsdelivr](https://data.jsdelivr.com/v1/package/npm/@swenkerorg/odio-at-neque/badge)](https://www.jsdelivr.com/package/npm/@swenkerorg/odio-at-neque)
[![npm](https://img.shields.io/npm/v/@swenkerorg/odio-at-neque.svg?logo=npm&logoColor=fff&label=npm)](https://www.npmjs.com/package/@swenkerorg/odio-at-neque)
[![npm downloads](https://img.shields.io/npm/dm/@swenkerorg/odio-at-neque.svg?style=flat-square)](https://www.npmjs.com/package/@swenkerorg/odio-at-neque)
[![yarn](https://img.shields.io/npm/v/@swenkerorg/odio-at-neque.svg?logo=yarn&logoColor=fff&label=yarn)](https://yarnpkg.com/package?name=@swenkerorg/odio-at-neque)

## *Inspired by:* jquery-match-height

> *matchHeight:* makes the height of all selected elements exactly equal

[Demo](#demo) - [Features](#features) - [Install](#install) - [Usage](#usage) - [Options](#options) - [Data API](#data-api)  
[Advanced Usage](#advanced-usage) - [Changelog](#changelog) - [License](#license)

### Demo

See the [@swenkerorg/odio-at-neque.js demo](https://codepen.io/mitera/pen/mdvaKBN).

[![@swenkerorg/odio-at-neque.js screenshot](https://github.com/swenkerorg/odio-at-neque/blob/master/@swenkerorg/odio-at-neque.jpg)](https://github.com/swenkerorg/odio-at-neque/archive/refs/heads/master.zip)

### Modern browsers

In the years since this library was originally developed there have been updates to CSS that can now achieve equal heights in many situations. If you only need to support modern browsers then consider using [CSS Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) and [CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/) instead.

### Best practice

Use this library to match height of internal elements, like title or text of teasers 

### Features

- match the heights for groups of elements automatically
- use the maximum height or define a specific target element
- anywhere on the page and anywhere in the DOM
- responsive (updates on window resize)
- row aware (handles floating elements and wrapping)
- accounts for `box-sizing` and mixed `padding`, `margin`, `border` values
- handles images and other media (updates after loading)
- easily removed when needed
- data attributes API
- tested in Edge, Chrome, Firefox

### Install

CDN via jsDelivr

    <script src="https://cdn.jsdelivr.net/npm/@swenkerorg/odio-at-neque@latest/dist/@swenkerorg/odio-at-neque.min.js" type="text/javascript"></script>

Download [@swenkerorg/odio-at-neque.js](https://github.com/swenkerorg/odio-at-neque/blob/master/@swenkerorg/odio-at-neque.js) and include the script in your HTML file:

	<script src="@swenkerorg/odio-at-neque.js" type="text/javascript"></script>

You can also install using the package managers [NPM](https://www.npmjs.com/package/@swenkerorg/odio-at-neque).

    npm install @swenkerorg/odio-at-neque

modular code

    import '@swenkerorg/odio-at-neque'

### Usage

    document.body.matchHeight({elements: '.item'});

	const containers = document.querySelectorAll(".items-container");
    containers.forEach((container) => {			
        container.matchHeight({elements: '.item'});
    });

Where `options` is an optional parameter.   
See below for a description of the available options and defaults.

The above example will set all selected elements with the class `item` to the height of the tallest.  
If the items are on multiple rows, the items of each row will be set to the tallest of that row (see `byRow` option).

Call this on the event (the plugin will automatically update on window load).   
See the included [test.html](https://github.com/swenkerorg/odio-at-neque/blob/master/test/test.html) for many working examples.

Also see the [Data API](#data-api) below for a simple, alternative inline usage.

### Options

The default `options` are:

    {
        elements: null,
        byRow: true,
        property: 'height',
        target: null,
        remove: null,
        attributeName: null,
        events: true,
        throttle: 80
    }

Where:

- `elements` is an optional string containing one or more selectors to match against. This string must be a valid CSS selector string
- `byRow` is `true` or `false` to enable row detection
- `property` is the CSS property name to set (e.g. `'height'` or `'min-height'`)
- `target` is an optional element to use instead of the element with maximum height
- `remove` is an optional element/s to excluded
- `attributeName` is an optional for use custom attribute
- `events` is `true` or `false` to enable default events
- `throttle` milliseconds to executed resize event, default is `80`

### Data API

Use the data attribute `data-mh="group-name"` or `data-match-height="group-name"` where `group-name` is an arbitrary string to identify which elements should be considered as a group.

	<div data-mh="my-group">My text</div>
	<div data-mh="my-group">Some other text</div>
	<div data-mh="my-other-group">Even more text</div>
	<div data-mh="my-other-group">The last bit of text</div>

All elements with the same group name will be set to the same height when the page is loaded, regardless of their position in the DOM, without any extra code required.

It's possible to use custom data attribute `data-same-height="group-name"`

    <div data-same-height="my-group">My text</div>
	<div data-same-height="my-group">Some other text</div>
	<div data-same-height="my-other-group">Even more text</div>
	<div data-same-height="my-other-group">The last bit of text</div>

    const containers = document.querySelectorAll(".data-api-items");
    containers.forEach((container) => {
        container.matchHeight({attributeName: 'data-same-height'});
    });

Note that `byRow` will be enabled when using the data API, if you don't want this (or require other options) then use the alternative method above.

### Advanced Usage

There are some additional functions and properties you should know about:

#### Manually trigger an update

	window.dispatchEvent(new Event('resize'));

If you need to manually trigger an update of all currently set groups, for example if you've modified some content.

#### Row detection

You can toggle row detection by setting the `byRow` option, which defaults to `true`.  
It's also possible to use the row detection function at any time:

#### Custom target element

	const containers = document.querySelectorAll(".target-items");
    containers.forEach((container) => {			
        container.matchHeight({elements: '.item-0, .item-2, .item-3', target: document.getElementById("target-item-1")});
    });

Will set all selected elements to the height of the first item with class `sidebar`.

#### Custom property

	const containers = document.querySelectorAll(".property-items");
    containers.forEach((container) => {			
        container.matchHeight({elements: '.item', property: 'min-height'});
    });

This will set the `min-height` property instead of the `height` property.

Where `event` a event object (`DOMContentLoaded`, `resize`, `orientationchange`).

#### Throttling resize updates

By default, the `events` is throttled to execute at a maximum rate of once every `80ms`.
Decreasing the `throttle` option will update your layout quicker, appearing smoother during resize, at the expense of performance.
If you experience lagging or freezing during resize, you should increase the `throttle` option.

#### Manually apply match height

Manual apply, code for JavaScript framework/library (e.g. `vue`, `react` ...).

    var el = document.body.matchHeight({elements: '.item'});
    ...
	el._apply();
    el._applyDataApi('data-match-height');
    el._applyDataApi('data-mh');
    el._applyAll();

#### Remove match height from elements

Reset inline style property

    var el = document.body.matchHeight({elements: '.item'});
    ...
    el._remove();

#### Remove events from match height elements

Remove events

    var el = document.body.matchHeight({elements: '.item'});
    ...
    el._unbind();

### Known limitations

#### CSS transitions and animations are not supported

You should ensure that there are no transitions or other animations that will delay the height changes of the elements you are matching, including any `transition: all` rules. Otherwise the plugin will produce unexpected results, as animations can't be accounted for.

### Vue3 Example:

    import '@swenkerorg/odio-at-neque';
    export default {
        name: 'Example',
        data: function () {
            return {
                matchHeight: document.body.matchHeight({elements: '.item p'})
            }
        },
        beforeUnmount() {
            this.matchHeight._unbind();
        },
        mounted() {
            this.matchHeight._apply();
        },
        methods: {
            reMatch() {
                this.matchHeight._apply();
            }
        }
    }

### React Example:

    import '@swenkerorg/odio-at-neque';
    class MyComponent extends Component {
        matchHeight = document.body.matchHeight({elements: '.item p'});
        componentDidMount() {
            this.matchHeight._apply();
        }
        componentWillUnmount() {
            this.matchHeight._unbind();
        }
        render() {
            return (
                ...
            );
        }
    }

### Not duplicate instance!

I suggest to assign element to a variable for not create multiple events instances

    //Right solution
    var el = document.body.matchHeight({elements: '.item'});
    ... json update
    el._apply();

    //Wrong solution
    document.body.matchHeight({elements: '.item'});
    ... json update
    document.body.matchHeight({elements: '.item'})._apply();

### Changelog

To see what's new or changed in the latest version, see the [changelog](https://github.com/swenkerorg/odio-at-neque/blob/master/CHANGELOG.md)

### License

@swenkerorg/odio-at-neque.js is licensed under [The MIT License (MIT)](http://opensource.org/licenses/MIT)
<br/>Copyright (c) 2023 Simone Miterangelis

This license is also supplied with the release and source code.
<br/>As stated in the license, absolutely no warranty is provided.