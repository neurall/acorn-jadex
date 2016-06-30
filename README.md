# Acorn-JadeX

This is my blatant fork of awesome Acorn-Jsx that served as base for great babej jsx transformation for React library.

Why ?

In short:

	"JSX / html ending tags eat 50% of precious space yet are absolutely not needed"

Indentation is our friend as Coffescript and Python show us every day.

So why dont write React apps more efficiently. Ie
You write like before = all JSX language features stay since parser is the same. 
just indentation now replaces the need of end tags
~~~~~~html
  <responsive drawer>

   <menu>
    <menuitem1>
    <menuitem2>
    <menuitem3>

   <content>
    <page1>
    <page2>    
    <page3>
~~~~~~
instead of noisy hard to understand
~~~~~~html
  <responsive drawer>
   <menu>
    <menuitem1>
    </menuitem1>
    <menuitem2>
    </menuitem2>
    <menuitem3>
    </menuitem3>
   </menu>
   <content>
    <page1>
    </page1>
    <page2>    
    </page2>
    <page3>
    </page3>
   </content>
  </responsive drawer>
~~~~~~

Well the idea to keep html tags css and js in one place so it is 
easy to see and understand "what looks how and when in small component focused file" is nowadays more important than ever.
especially after years of fragmented impossible to maintainn mega monsters. 

Wait! Isnt there already Jade templating language for that ?

Yes but it forces you to again separate html and code. It intruduces yet another custom language for what js does better.
You cant have clear easy to read es6 arrows imports intermixed with html tags like JSX does.
also being able to distinguish what is visual part = `<div>` instead of `div` and what is variable / code is important too.

Main problem with HTML are noisy end tags.

Problem with html is that like XML it is unnecesarily noisy. And as the project grows you loose advantages that led you
to mixing html with js in first place. 
Ie ability to keep you focused on what is being rendered



Goal:

I hope to produce patch to babel soon since it was based on accorn-jsx.
But right now babel is so fragmented so i have no ide what version to patch. ver 5 ? v 6 ?
Hopefully some more skilled folks will help ;)


---- End of my shameless doc plug ---

[![Build Status](https://travis-ci.org/RReverser/acorn-jsx.svg?branch=master)](https://travis-ci.org/RReverser/acorn-jsx)
[![NPM version](https://img.shields.io/npm/v/acorn-jsx.svg)](https://www.npmjs.org/package/acorn-jsx)

This is plugin for [Acorn](http://marijnhaverbeke.nl/acorn/) - a tiny, fast JavaScript parser, written completely in JavaScript.

It was created as an experimental alternative, faster [React.js JSX](http://facebook.github.io/react/docs/jsx-in-depth.html) parser.

According to [benchmarks](https://github.com/RReverser/acorn-jsx/blob/master/test/bench.html), Acorn-JSX is 2x faster than official [Esprima-based parser](https://github.com/facebook/esprima) when location tracking is turned on in both (call it "source maps enabled mode"). At the same time, it consumes all the ES6+JSX syntax that can be consumed by Esprima-FB (this is proved by [official tests](https://github.com/RReverser/acorn-jsx/blob/master/test/tests-jsx.js)).

**UPDATE [14-Apr-2015]**: Facebook implementation started [deprecation process](https://github.com/facebook/esprima/issues/111) in favor of Acorn + Acorn-JSX + Babel for parsing and transpiling JSX syntax.

## Transpiler

Please note that this tool only parses source code to JSX AST, which is useful for various language tools and services. If you want to transpile your code to regular ES5-compliant JavaScript with source map, check out the [babel transpiler](https://babeljs.io/) which uses `acorn-jsx` under the hood.

## Usage

You can use module directly in order to get Acorn instance with plugin installed:

```javascript
var acorn = require('acorn-jsx');
```

Or you can use `inject.js` for injecting plugin into your own version of Acorn like following:

```javascript
var acorn = require('acorn-jsx/inject')(require('./custom-acorn'));
```

Then, use `plugins` option whenever you need to support JSX while parsing:

```javascript
var ast = acorn.parse(code, {
  plugins: { jsx: true }
});
```

Note that official spec doesn't support mix of XML namespaces and object-style access in tag names (#27) like in `<namespace:Object.Property />`, so it was deprecated in `acorn-jsx@3.0`. If you still want to opt-in to support of such constructions, you can pass the following option:

```javascript
var ast = acorn.parse(code, {
  plugins: {
    jsx: { allowNamespacedObjects: true }
  }
});
```

Also, since most apps use pure React transformer, a new option was introduced that allows to prohibit namespaces completely:

```javascript
var ast = acorn.parse(code, {
  plugins: {
    jsx: { allowNamespaces: false }
  }
});
```

Note that by default `allowNamespaces` is enabled for spec compliancy.

## License

This plugin is issued under the [MIT license](./LICENSE).
