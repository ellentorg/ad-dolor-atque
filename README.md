# @ellentorg/ad-dolor-atque

[![NPM](https://nodei.co/npm/@ellentorg/ad-dolor-atque.png)](https://nodei.co/npm/@ellentorg/ad-dolor-atque/)

[![NPM version](https://badgen.net/npm/v/@ellentorg/ad-dolor-atque)](https://www.npmjs.com/package/@ellentorg/ad-dolor-atque)
[![Bundlephobia minified + gzip](https://badgen.net/bundlephobia/minzip/@ellentorg/ad-dolor-atque)](https://bundlephobia.com/package/@ellentorg/ad-dolor-atque)
[![build](https://github.com/ellentorg/ad-dolor-atque/actions/workflows/build.yml/badge.svg)](https://github.com/ellentorg/ad-dolor-atque/actions/workflows/build.yml)
[![codecov](https://codecov.io/gh/remarkablemark/@ellentorg/ad-dolor-atque/branch/master/graph/badge.svg?token=JWKUKTFT3E)](https://codecov.io/gh/remarkablemark/@ellentorg/ad-dolor-atque)
[![NPM downloads](https://badgen.net/npm/dm/@ellentorg/ad-dolor-atque)](https://www.npmjs.com/package/@ellentorg/ad-dolor-atque)

Parses CSS inline style to JavaScript object (camelCased):

```
StyleToJS(string)
```

## Example

```js
import parse from '@ellentorg/ad-dolor-atque';

parse('background-color: #BADA55;');
```

Output:

```json
{ "backgroundColor": "#BADA55" }
```

[Replit](https://replit.com/@remarkablemark/@ellentorg/ad-dolor-atque) | [JSFiddle](https://jsfiddle.net/remarkablemark/04nob1y7/) | [Examples](https://github.com/ellentorg/ad-dolor-atque/tree/master/examples)

## Install

[NPM](https://www.npmjs.com/package/@ellentorg/ad-dolor-atque):

```sh
npm install @ellentorg/ad-dolor-atque --save
```

[Yarn](https://yarnpkg.com/package/@ellentorg/ad-dolor-atque):

```sh
yarn add @ellentorg/ad-dolor-atque
```

[CDN](https://unpkg.com/@ellentorg/ad-dolor-atque/):

```html
<script src="https://unpkg.com/@ellentorg/ad-dolor-atque@latest/umd/@ellentorg/ad-dolor-atque.min.js"></script>
<script>
  window.StyleToJS(/* string */);
</script>
```

## Usage

### Import

Import with ES Modules:

```js
import parse from '@ellentorg/ad-dolor-atque';
```

Require with CommonJS:

```js
const parse = require('@ellentorg/ad-dolor-atque');
```

### Parse style

Parse single declaration:

```js
parse('line-height: 42');
```

Output:

```json
{ "lineHeight": "42" }
```

> Notice that the CSS property is camelCased.

Parse multiple declarations:

```js
parse(`
  border-color: #ACE;
  z-index: 1337;
`);
```

Output:

```json
{
  "borderColor": "#ACE",
  "zIndex": "1337"
}
```

### Vendor prefix

Parse [vendor prefix](https://developer.mozilla.org/en-US/docs/Glossary/Vendor_Prefix):

```js
parse(`
  -webkit-transition: all 4s ease;
  -moz-transition: all 4s ease;
  -ms-transition: all 4s ease;
  -o-transition: all 4s ease;
  -khtml-transition: all 4s ease;
`);
```

Output:

```json
{
  "webkitTransition": "all 4s ease",
  "mozTransition": "all 4s ease",
  "msTransition": "all 4s ease",
  "oTransition": "all 4s ease",
  "khtmlTransition": "all 4s ease"
}
```

### Custom property

Parse [custom property](https://developer.mozilla.org/en-US/docs/Web/CSS/--*):

```js
parse('--custom-property: #f00');
```

Output:

```json
{ "--custom-property": "#f00" }
```

### Unknown declaration

This library does not validate declarations, so unknown declarations can be parsed:

```js
parse('the-answer: 42;');
```

Output:

```json
{ "theAnswer": "42" }
```

### Invalid declaration

Declarations with missing value are removed:

```js
parse(`
  margin-top: ;
  margin-right: 1em;
`);
```

Output:

```json
{ "marginRight": "1em" }
```

Other invalid declarations or arguments:

```js
parse(); // {}
parse(null); // {}
parse(1); // {}
parse(true); // {}
parse('top:'); // {}
parse(':12px'); // {}
parse(':'); // {}
parse(';'); // {}
```

The following values will throw an error:

```js
parse('top'); // Uncaught Error: property missing ':'
parse('/*'); // Uncaught Error: End of comment missing
```

### Options

#### reactCompat

When option `reactCompat` is true, the [vendor prefix](https://developer.mozilla.org/en-US/docs/Glossary/Vendor_Prefix) will be capitalized:

```js
parse(
  `
    -webkit-transition: all 4s ease;
    -moz-transition: all 4s ease;
    -ms-transition: all 4s ease;
    -o-transition: all 4s ease;
    -khtml-transition: all 4s ease;
  `,
  { reactCompat: true },
);
```

Output:

```json
{
  "WebkitTransition": "all 4s ease",
  "MozTransition": "all 4s ease",
  "msTransition": "all 4s ease",
  "OTransition": "all 4s ease",
  "KhtmlTransition": "all 4s ease"
}
```

This removes the React warning:

```
Warning: Unsupported vendor-prefixed style property %s. Did you mean %s?%s", "oTransition", "OTransition"
```

## Testing

Run tests with coverage:

```sh
npm test
```

Run tests in watch mode:

```sh
npm run test:watch
```

Lint files:

```sh
npm run lint
```

Fix lint errors:

```sh
npm run lint:fix
```

## Release

Release and publish are automated by [Release Please](https://github.com/googleapis/release-please).

## Special Thanks

- [style-to-object](https://github.com/remarkablemark/style-to-object)

## License

[MIT](https://github.com/ellentorg/ad-dolor-atque/blob/master/LICENSE)
