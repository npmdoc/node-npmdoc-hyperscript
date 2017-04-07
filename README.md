# api documentation for  [hyperscript (v2.0.2)](https://github.com/dominictarr/hyperscript)  [![npm package](https://img.shields.io/npm/v/npmdoc-hyperscript.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-hyperscript) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-hyperscript.svg)](https://travis-ci.org/npmdoc/node-npmdoc-hyperscript)
#### Create HyperText with JavaScript, on client or server.

[![NPM](https://nodei.co/npm/hyperscript.png?downloads=true)](https://www.npmjs.com/package/hyperscript)

[![apidoc](https://npmdoc.github.io/node-npmdoc-hyperscript/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-hyperscript_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-hyperscript/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-hyperscript/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-hyperscript/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "'Dominic Tarr'",
        "email": "dominic.tarr@gmail.com",
        "url": "http://dominictarr.com"
    },
    "browser": {
        "html-element": false
    },
    "bugs": {
        "url": "https://github.com/dominictarr/hyperscript/issues"
    },
    "dependencies": {
        "browser-split": "0.0.0",
        "class-list": "~0.1.0",
        "html-element": "^2.0.0"
    },
    "description": "Create HyperText with JavaScript, on client or server.",
    "devDependencies": {
        "ispy": "~0.1.2",
        "observable": "~2.1.2",
        "simulate": "0.0.3",
        "tape": "~2.13.3"
    },
    "directories": {},
    "dist": {
        "shasum": "3839cba45554bdfe27bb81c2142d1684f8135af5",
        "tarball": "https://registry.npmjs.org/hyperscript/-/hyperscript-2.0.2.tgz"
    },
    "gitHead": "81914f9b54347093343d5683c5533f7fcd342967",
    "homepage": "https://github.com/dominictarr/hyperscript",
    "license": "MIT",
    "maintainers": [
        {
            "name": "dominictarr",
            "email": "dominic.tarr@gmail.com"
        }
    ],
    "name": "hyperscript",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/dominictarr/hyperscript.git"
    },
    "scripts": {
        "test": "set -e; for t in test/*.js; do node $t; done"
    },
    "testling": {
        "files": "test/*.js",
        "browsers": [
            "ie/8..latest",
            "firefox/17..latest",
            "firefox/nightly",
            "chrome/22..latest",
            "chrome/canary",
            "opera/12..latest",
            "opera/next",
            "safari/5.1..latest",
            "ipad/6.0..latest",
            "iphone/6.0..latest",
            "android-browser/4.2..latest"
        ]
    },
    "version": "2.0.2"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module hyperscript](#apidoc.module.hyperscript)
1.  [function <span class="apidocSignatureSpan">hyperscript.</span>cleanup ()](#apidoc.element.hyperscript.cleanup)
1.  [function <span class="apidocSignatureSpan">hyperscript.</span>context ()](#apidoc.element.hyperscript.context)



# <a name="apidoc.module.hyperscript"></a>[module hyperscript](#apidoc.module.hyperscript)

#### <a name="apidoc.element.hyperscript.cleanup"></a>[function <span class="apidocSignatureSpan">hyperscript.</span>cleanup ()](#apidoc.element.hyperscript.cleanup)
- description and source-code
```javascript
cleanup = function () {
  for (var i = 0; i < cleanupFuncs.length; i++){
    cleanupFuncs[i]()
  }
  cleanupFuncs.length = 0
}
```
- example usage
```shell
...
    text('you are 1,000,000th visitor!')
    e.preventDefault()
  }
}, text)

// then if you want to remove this widget from the page
// to cleanup
h.cleanup()

'''
## Ecosystem

* [html2hscript](https://github.com/twilson63/html2hscript) - Parse HTML into hyperscript
* [dom2hscript](https://github.com/AkeemMcLennon/dom2hscript) - Frontend library for parsing HTML into hyperscript using the browser
's built in parser.
* [html2hscript.herokuapp.com](http://html2hscript.herokuapp.com/) - Online Tool that converts html snippets to hyperscript
...
```

#### <a name="apidoc.element.hyperscript.context"></a>[function <span class="apidocSignatureSpan">hyperscript.</span>context ()](#apidoc.element.hyperscript.context)
- description and source-code
```javascript
function context() {

  var cleanupFuncs = []

  function h() {
    var args = [].slice.call(arguments), e = null
    function item (l) {
      var r
      function parseClass (string) {
        // Our minimal parser doesn’t understand escaping CSS special
        // characters like '#'. Don’t use them. More reading:
        // https://mathiasbynens.be/notes/css-escapes .

        var m = split(string, /([\.#]?[^\s#.]+)/)
        if(/^\.|#/.test(m[1]))
          e = document.createElement('div')
        forEach(m, function (v) {
          var s = v.substring(1,v.length)
          if(!v) return
          if(!e)
            e = document.createElement(v)
          else if (v[0] === '.')
            ClassList(e).add(s)
          else if (v[0] === '#')
            e.setAttribute('id', s)
        })
      }

      if(l == null)
        ;
      else if('string' === typeof l) {
        if(!e)
          parseClass(l)
        else
          e.appendChild(r = document.createTextNode(l))
      }
      else if('number' === typeof l
        || 'boolean' === typeof l
        || l instanceof Date
        || l instanceof RegExp ) {
          e.appendChild(r = document.createTextNode(l.toString()))
      }
      //there might be a better way to handle this...
      else if (isArray(l))
        forEach(l, item)
      else if(isNode(l))
        e.appendChild(r = l)
      else if(l instanceof Text)
        e.appendChild(r = l)
      else if ('object' === typeof l) {
        for (var k in l) {
          if('function' === typeof l[k]) {
            if(/^on\w+/.test(k)) {
              (function (k, l) { // capture k, l in the closure
                if (e.addEventListener){
                  e.addEventListener(k.substring(2), l[k], false)
                  cleanupFuncs.push(function(){
                    e.removeEventListener(k.substring(2), l[k], false)
                  })
                }else{
                  e.attachEvent(k, l[k])
                  cleanupFuncs.push(function(){
                    e.detachEvent(k, l[k])
                  })
                }
              })(k, l)
            } else {
              // observable
              e[k] = l[k]()
              cleanupFuncs.push(l[k](function (v) {
                e[k] = v
              }))
            }
          }
          else if(k === 'style') {
            if('string' === typeof l[k]) {
              e.style.cssText = l[k]
            }else{
              for (var s in l[k]) (function(s, v) {
                if('function' === typeof v) {
                  // observable
                  e.style.setProperty(s, v())
                  cleanupFuncs.push(v(function (val) {
                    e.style.setProperty(s, val)
                  }))
                } else
                  var match = l[k][s].match(/(.*)\W+!important\W*$/);
                  if (match) {
                    e.style.setProperty(s, match[1], 'important')
                  } else {
                    e.style.setProperty(s, l[k][s])
                  }
              })(s, l[k][s])
            }
          } else if(k === 'attrs') {
            for (var v in l[k]) {
              e.setAttribute(v, l[k][v])
            }
          }
          else if (k.substr(0, 5) === "data-") {
            e.setAttribute(k, l[k])
          } else {
            e[k] = l[k]
          }
        }
      } else if ('function' === typeof l) {
        //assume it's an observable!
        var v = l()
        e.appendChild(r = isNode(v) ? v : document.createTextNode(v))

        cleanupFuncs.push(l(function (v) {
          if(isNode(v) && r.parentElement)
            r.parentElement.replaceChild(v, r), r = v
          else
            r.textContent = v
        }))
      }

      return r
    }
    while(args.length)
      item(args.shift())

    return e
  }

  h.cleanup = function () {
    for (var i = 0; i < cleanupFuncs.length; i++){
      cleanupFuncs[i]()
    }
    cleanupFuncs.length = 0
  }

  return h
}
```
- example usage
```shell
...
'''

### Cleaning Up

If you need to clean up a widget created using hyperscript - deregistering all its event handlers and observable listeners, you
can use 'context()'.

''' js
var h = require('hyperscript').context()
var o = require('observable')
var text = o()
text('click here to win a prize')
h('a', {href: '#',
onclick: function (e) {
  text('you are 1,000,000th visitor!')
  e.preventDefault()
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
