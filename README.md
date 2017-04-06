# api documentation for  [coffeeify (v2.1.0)](https://github.com/jnordberg/coffeeify)  [![npm package](https://img.shields.io/npm/v/npmdoc-coffeeify.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-coffeeify) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-coffeeify.svg)](https://travis-ci.org/npmdoc/node-npmdoc-coffeeify)
#### browserify plugin for coffee-script with support for mixed .js and .coffee files

[![NPM](https://nodei.co/npm/coffeeify.png?downloads=true)](https://www.npmjs.com/package/coffeeify)

[![apidoc](https://npmdoc.github.io/node-npmdoc-coffeeify/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-coffeeify_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-coffeeify/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-coffeeify/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-coffeeify/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "bugs": {
        "url": "https://github.com/jnordberg/coffeeify/issues"
    },
    "contributors": [
        {
            "name": "James Halliday",
            "email": "mail@substack.net",
            "url": "http://substack.net"
        },
        {
            "name": "Johan Nordberg",
            "email": "code@johan-nordberg.com",
            "url": "http://johan-nordberg.com"
        }
    ],
    "dependencies": {
        "coffee-script": "^1.12.0",
        "convert-source-map": "^1.3.0",
        "through2": "^2.0.0"
    },
    "description": "browserify plugin for coffee-script with support for mixed .js and .coffee files",
    "devDependencies": {
        "browserify": "^13.1.1",
        "tap": "^8.0.1",
        "through": "^2.3.8"
    },
    "directories": {},
    "dist": {
        "shasum": "06de80aa87b6194937734361def4ade254b71a1e",
        "tarball": "https://registry.npmjs.org/coffeeify/-/coffeeify-2.1.0.tgz"
    },
    "gitHead": "f2c99868d76e4ccf9cd1ef856d4c72f9a9026642",
    "homepage": "https://github.com/jnordberg/coffeeify",
    "keywords": [
        "coffee-script",
        "browserify",
        "v2",
        "js",
        "plugin",
        "transform"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "substack",
            "email": "mail@substack.net"
        },
        {
            "name": "jnordberg",
            "email": "its@johan-nordberg.com"
        }
    ],
    "name": "coffeeify",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/jnordberg/coffeeify.git"
    },
    "scripts": {
        "test": "tap test/*.js"
    },
    "version": "2.1.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module coffeeify](#apidoc.module.coffeeify)
1.  [function <span class="apidocSignatureSpan">coffeeify.</span>compile (filename, source, options, callback)](#apidoc.element.coffeeify.compile)
1.  [function <span class="apidocSignatureSpan">coffeeify.</span>isCoffee (file)](#apidoc.element.coffeeify.isCoffee)
1.  [function <span class="apidocSignatureSpan">coffeeify.</span>isLiterate (file)](#apidoc.element.coffeeify.isLiterate)



# <a name="apidoc.module.coffeeify"></a>[module coffeeify](#apidoc.module.coffeeify)

#### <a name="apidoc.element.coffeeify.compile"></a>[function <span class="apidocSignatureSpan">coffeeify.</span>compile (filename, source, options, callback)](#apidoc.element.coffeeify.compile)
- description and source-code
```javascript
function compile(filename, source, options, callback) {
    var compiled;
    try {
        compiled = coffee.compile(source, {
            sourceMap: options.sourceMap,
            inline: true,
            bare: options.bare,
            header: options.header,
            literate: isLiterate(filename)
        });
    } catch (e) {
        var error = e;
        if (e.location) {
            error = new ParseError(e, source, filename);
        }
        callback(error);
        return;
    }

    if (options.sourceMap) {
        var map = convert.fromJSON(compiled.v3SourceMap);
        var basename = path.basename(filename);
        map.setProperty('file', basename.replace(filePattern, '.js'));
        map.setProperty('sources', [basename]);
        map.setProperty('sourcesContent', [source]);
        callback(null, compiled.js + '\n' + map.toComment() + '\n');
    } else {
        callback(null, compiled + '\n');
    }

}
```
- example usage
```shell
...
ParseError.prototype.inspect = function () {
return this.annotated;
};

function compile(filename, source, options, callback) {
var compiled;
try {
    compiled = coffee.compile(source, {
        sourceMap: options.sourceMap,
        inline: true,
        bare: options.bare,
        header: options.header,
        literate: isLiterate(filename)
    });
} catch (e) {
...
```

#### <a name="apidoc.element.coffeeify.isCoffee"></a>[function <span class="apidocSignatureSpan">coffeeify.</span>isCoffee (file)](#apidoc.element.coffeeify.isCoffee)
- description and source-code
```javascript
function isCoffee(file) {
    return filePattern.test(file);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.coffeeify.isLiterate"></a>[function <span class="apidocSignatureSpan">coffeeify.</span>isLiterate (file)](#apidoc.element.coffeeify.isLiterate)
- description and source-code
```javascript
function isLiterate(file) {
    return (/\.(litcoffee|coffee\.md)$/).test(file);
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
