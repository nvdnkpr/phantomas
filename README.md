phantomas
=========

![GitHub Logo](http://upload.wikimedia.org/wikipedia/en/a/a5/Fantomas.jpg)

PhantomJS-based modular web performance metrics collector. And why phantomas? Well, [because](http://en.wikipedia.org/wiki/Fantômas) :)

[![NPM version](https://badge.fury.io/js/phantomas.png)](http://badge.fury.io/js/phantomas)
[![Build Status](https://api.travis-ci.org/macbre/phantomas.png)](http://travis-ci.org/macbre/phantomas)

## Requirements

* [PhantomJS 1.9+](http://phantomjs.org/)
* [NodeJS](http://nodejs.org) (for `run-multiple.js` script and `--analyze-css` option)

## Installation

```
npm install --global phantomas
```

> This will add a symlink called ``phantomas`` (pointing to ``./phantomas.js``) to your system's ``PATH``

## Dependencies

phantomas uses the following 3rd party libraries (located in `/lib` directory):

* CommonJS modules from [phantomjs-nodify](https://github.com/jgonera/phantomjs-nodify) and nodejs source

## Let's make Web a bit faster!

* [Best Practices for Speeding Up Your Web Site](http://developer.yahoo.com/performance/rules.html) (by Yahoo!)
* [Web Performance Best Practices](https://developers.google.com/speed/docs/best-practices/rules_intro) (by Google)
* [Writing Efficient CSS](http://developer.mozilla.org/en/Writing_Efficient_CSS) (by Mozilla)
* [Planet Performance](http://www.perfplanet.com/) - news and views from the web performance blogosphere

### Slides
 
* [Know Your Engines: How to Make Your JavaScript Fast](http://cdn.oreillystatic.com/en/assets/1/event/60/Know%20Your%20Engines_%20How%20to%20Make%20Your%20JavaScript%20Fast%20Presentation%201.pdf) (by David Mandelin from Mozilla)


## Contributors

* [macbre](https://github.com/macbre)
* [jmervine](https://github.com/jmervine)
* [jmosney](https://github.com/jmosney)
* [umaar](https://github.com/umaar)
* [sjhcockrell](https://github.com/sjhcockrell)
* All the [contributors](https://github.com/macbre/phantomas/graphs/contributors)

## Usage

### Single run

``` bash
phantomas --url https://github.com/macbre/phantomas --verbose
```

You can measure the performance of your site without requests to 3rd party domains (but allowing CDN that serves your static assets):

```bash
phantomas --url https://github.com/macbre/phantomas --verbose --no-externals --allow-domain .fastly.net
```

#### Parameters

* `--url` URL of the page to generate metrics for (required)
* `--format=[json|csv|plain]` output format (``plain`` is the default one)
* `--timeout=[seconds]` timeout for phantomas run (defaults to 15 seconds)
* `--viewport=[width]x[height]` phantomJS viewport dimensions (1280x1024 is the default)
* `--verbose` writes debug messages to the console
* `--silent` don't write anything to the console
* `--log=[log file]` log to a given file
* `--modules=[moduleOne],[moduleTwo]` run only selected modules
* `--skip-modules=[moduleOne],[moduleTwo]` skip selected modules
* `--user-agent='Custom user agent'` provide a custom user agent (will default to something similar to ``phantomas/0.6.0 (PhantomJS/1.9.0; linux 64bit)``)
* `--config=[JSON config file]` uses JSON-formatted config file to set parameters
* `--cookie='bar=foo;domain=url'` document.cookie formatted string for setting a single cookie
* `--no-externals` block requests to 3rd party domains
* `--allow-domain=[domain],[domain]` allow requests to given domai(s) - aka whitelist
* `--block-domain=[domain],[domain]` disallow requests to given domai(s) - aka blacklist
* `--analyze-css` emit in-depth CSS metrics

### Multiple runs

This helper script requires NodeJS.

``` bash
./run-multiple.js --url=https://github.com/macbre/phantomas  --runs=5
```

#### Parameters

* `--url` URL of the page to generate metrics for (required)
* `--runs` number of runs to perform (defaults to 3)
* `--modules=[moduleOne],[moduleTwo]` run only selected modules
* `--skip-modules=[moduleOne],[moduleTwo]` skip selected modules

## Features

* Modular approach - each metric is generated by a separate "module"
* phantomas "core" acts as an [events emitter](https://github.com/macbre/phantomas/wiki/Events) that each module can hook into
* JSON and CSV as available output formats for easy integration with automated reporting / monitoring tools
* Utilities:
 * helper script to run phantomas multiple times
 * CSS analyzer

## Metrics

_Current number of metrics: 90_

Units:

* ms for time
* bytes for size

``` 
$ phantomas --url https://github.com/macbre/phantomas

phantomas metrics for <https://github.com/macbre/phantomas>:

* requests: 15
* gzipRequests: 8
* postRequests: 0
* httpsRequests: 15
* redirects: 1
* notFound: 0
* timeToFirstByte: 722
* timeToLastByte: 730
* bodySize: 394612
* contentLength: 420351
* ajaxRequests: 0
* htmlCount: 1
* htmlSize: 68335
* cssCount: 2
* cssSize: 163237
* jsCount: 4
* jsSize: 115046
* jsonCount: 0
* jsonSize: 0
* imageCount: 7
* imageSize: 24514
* webfontCount: 1
* webfontSize: 23480
* base64Count: 0
* base64Size: 0
* otherCount: 0
* otherSize: 0
* cacheHits: 9
* cacheMisses: 0
* cachingNotSpecified: 4
* cachingTooShort: 3
* cachingDisabled: 0
* domains: 8
* maxRequestsPerDomain: 7
* medianRequestsPerDomain: 1.5
* DOMqueries: 90
* DOMqueriesById: 17
* DOMqueriesByClassName: 52
* DOMqueriesByTagName: 21
* DOMqueriesByQuerySelectorAll: 0
* DOMinserts: 16
* DOMqueriesDuplicated: 10
* eventsBound: 119
* headersCount: 264
* headersSentCount: 44
* headersRecvCount: 220
* headersSize: 8922
* headersSentSize: 1829
* headersRecvSize: 7093
* documentWriteCalls: 0
* evalCalls: 0
* jQueryVersion: 2.0.0
* jQueryOnDOMReadyFunctions: 42
* jQuerySizzleCalls: 92
* assetsNotGzipped: 1
* assetsWithQueryString: 4
* smallImages: 4
* multipleRequests: 0
* timeToFirstCss: 1069
* timeToFirstJs: 1407
* timeToFirstImage: 1994
* onDOMReadyTime: 204
* windowOnLoadTime: 5526
* httpTrafficCompleted: 7089
* windowAlerts: 0
* windowConfirms: 0
* windowPrompts: 0
* consoleMessages: 0
* cookiesSent: 0
* cookiesRecv: 492
* domainsWithCookies: 2
* documentCookiesLength: 268
* documentCookiesCount: 8
* bodyHTMLSize: 64146
* iframesCount: 0
* imagesWithoutDimensions: 2
* commentsSize: 245
* hiddenContentSize: 9933
* whiteSpacesSize: 3277
* DOMelementsCount: 831
* DOMelementMaxDepth: 12
* nodesWithInlineCSS: 5
* globalVariables: 23
* jsErrors: 0
* localStorageEntries: 0
* smallestResponse: 35
* biggestResponse: 82544
* fastestResponse: 41
* slowestResponse: 5323
* medianResponse: 429.5
```

### Requests monitor (core module)

* requests: total number of HTTP requests made
* gzipRequests: number of gzipped HTTP responses
* postRequests: number of POST requests
* httpsRequests: number of HTTPS requests
* redirects: number of HTTP redirects (either 301 or 302)
* notFound: number of HTTP 404 responses
* timeToFirstByte: time it took to receive the first byte of the first response
* timeToLastByte: time it took to receive the last byte of the first response
* bodySize: size of the content of all responses
* contentLength: size of the content of all responses (based on ``Content-Length`` header)
* httpTrafficCompleted: time it took to receive the last byte of the last HTTP response

### AJAX requests

* ajaxRequests: number of AJAX requests

### Assets types

* htmlCount: number of HTML responses
* htmlSize: size of HTML responses
* cssCount: number of CSS responses
* cssSize: size of CSS responses
* jsCount: number of JS responses
* jsSize: size of JS responses
* jsonCount: number of JSON responses
* jsonSize: size of JSON responses
* imageCount: number of image responses
* imageSize: size of image responses
* webfontCount: number of web font responses
* webfontSize: size of web font responses
* base64Count: number of base64 encoded "responses" (no HTTP request was actually made)
* base64Size: size of base64 encoded "responses"
* otherCount: number of other responses
* otherSize: size of other responses

### Cache Hits

_Metrics are calculated based on ``X-Cache`` header added by Varnish  / Squid servers._

* cacheHits: number of cache hits
* cacheMisses: number of cache misses

### Headers

* headersCount: number of requests and responses headers
* headersSentCount: number of headers sent in requests
* headersRecvCount: number of headers received in responses
* headersSize: size of all headers
* headersSentSize: size of sent headers
* headersRecvSize: size of received headers

### Domains

* domains: number of domains used to fetch the page
* maxRequestsPerDomain: maximum number of requests fetched from a single domain
* medianRequestsPerDomain: median of requests fetched from each domain

### Cookies

* cookiesSent: length of cookies sent in HTTP requests
* cookiesRecv: length of cookies received in HTTP responses
* domainsWithCookies: number of domains with cookies set
* documentCookiesLength: length of `document.cookie`
* documentCookiesCount: number of cookies in `document.cookie`

### DOM complexity

* globalVariables: number of JS globals variables
* bodyHTMLSize: the size of body tag content
* commentsSize: the size of HTML comments on the page
* hiddenContentSize: the size of content of hidden elements on the page (with CSS ``display: none``)
* whiteSpacesSize: the size of text nodes with whitespaces only
* DOMelementsCount: total number of HTML element nodes
* DOMelementMaxDepth: maximum level on nesting of HTML element node
* iframesCount: number of iframe nodes
* nodesWithInlineCSS: number of nodes with inline CSS styling (with `style` attribute)
* imagesWithoutDimensions: number of ``<img>`` nodes without both ``width`` and ``height`` attribute

### DOM queries

* DOMqueries: the sum of all four metrics below
* DOMqueriesById: number of `document.getElementById` calls
* DOMqueriesByClassName: number of `document.getElementsByClassName` calls
* DOMqueriesByTagName: number of `document.getElementsByTagName` calls
* DOMqueriesByQuerySelectorAll: number of `document.querySelectorAll` calls
* DOMinserts: number of DOM nodes inserts
* DOMqueriesDuplicated: number of duplicated DOM queries

### Event listeners

* eventsBound: number of ``EventTarget.addEventListener`` calls

### Window performance

* onDOMReadyTime: time it took to fire onDOMready event
* windowOnLoadTime: time it took to fire window.load event

### Requests statistics

* smallestResponse: the size of the smallest response
* biggestResponse: the size of the biggest response
* fastestResponse: the time to the last byte of the fastest response
* slowestResponse: the time to the last byte of the slowest response
* medianResponse: median value of time to the last byte for all responses

### localStorage

* localStorageEntries: number of entries in local storage

### jQuery

* jQueryVersion: version of jQuery framework (if loaded)
* jQueryOnDOMReadyFunctions: number of functions bound to onDOMReady event
* jQuerySizzleCalls: number of calls to [Sizzle](http://sizzlejs.com/) (including those that will be resolved using ``querySelectorAll``)

### Static assets

* assetsNotGzipped: static assets that were not gzipped
* assetsWithQueryString: static assets requested with query string (e.g. ?foo) in URL
* smallImages: images smaller than 2 kB that can be base64 encoded
* multipleRequests: number of static assets that are requested more than once

### Caching

* cachingNotSpecified: responses with no caching header sent (either `Cache-Control` or `Expires`)
* cachingTooShort: responses with too short (less than a week) caching time
* cachingDisabled: responses with caching disabled (`max-age=0`)

### Time to first asset

* timeToFirstCss: time it took to receive the last byte of the first CSS
* timeToFirstJs: time it took to receive the last byte of the first JS
* timeToFirstImage: time it took to receive the last byte of the first image

### JavaScript bottlenecks

* documentWriteCalls: number of calls to either ``document.write`` or ``document.writeln``
* evalCalls: number of calls to ``eval`` (either direct or via ``setTimeout`` / ``setInterval``)

### JavaScript errors

* jsErrors: number of JavaScript errors

### JavaScript console and alert

* windowAlerts: number of calls to ``alert``
* windowConfirms: number of calls to ``confirm``
* windowPrompts: number of calls to ``prompt``
* consoleMessages: number of calls to ``console.*`` functions

### CSS metrics

> This is an experimental feature. Use `--analyze-css` option to enable it.

* cssLength: total length of all analyzed CSS files (including comments and whitespaces)
* cssSelectorsTotal: total number of selectors (`.foo, .bar` counts as two)
* cssSelectorsPartsTotal: total number of selectors parts (`ul > .bar > a` counts as three)
* cssDeclarationsTotal: total number of properties defined in CSS file
* cssEmptyDeclarations: total number of selectors with no properties defined (`.foo { }`)
* cssComplexSelectors: number of complex selectors (consisting of three or more parts)
* cssQualifiedRules: number of selectors that are mix of either ID and tag name, ID and class or class and tag name
* cssOldIEFixes: hacky fixes for old versions of Internet Explorer including:
 * number of properties that are prefixed with asterisk (hacky fix for IE7 and below)
 * number of selectors starting with `* html` (hacky fix for IE6 and below)
* cssSelectorsByTag: number of selectors by tag name
* cssSelectorsByWildcard: number of selectors matching all tags (`nav *`)
* cssSelectorsByClass: number of selectors by class
* cssSelectorsById: number of selectors by ID
* cssSelectorsByPseudo: number of pseudo-selectors (`:hover`)
* cssSelectorsByAttribute: number of selectors by attribute (`.foo[value=bar]`)
* cssSelectorsByAttributeComplex: number of selectors by attribute's value with "regular expressions matching" (`img[src$=.jpg]`)
* cssImportantsTotal: number of properties with value forced by `!important`

## Debug logs and notices

phantomas apart from "raw" metrics data, when in `--verbose` mode, emits debug logs and notices with more in-depth data:

```
21:20:04.553 Sizzle called: .mfbb .frm:not(.fst) (context: #document)
21:20:08.309 DOM insert: node "script" added to "head"
21:26:52.348 eval() called directly: from unknown fn: http://lib.onet.pl/s.csr/init/20130829,init.js @ 53!
21:26:52.348 Backtrace: unknown fn: http://lib.onet.pl/s.csr/init/20130829,init.js @ 53 / onetShowAsyncSlots(): http://lib.onet.pl/s.csr/init/20130829,init.js @ 18 / onetShowAsynchAds(): http://lib.onet.pl/s.csr/init/20130829,init.js @ 15 / unknown fn: http://csr.onet.pl/_s/csr-005/GLOWNA/NOWASG/slots=top,right,flat-sidebarbox,flat-search,flat-boks1,flat-link1,flat-link2,flat-link3,flat-link5,flat-link4,flat-link6,flat-link7,flat-link8,flat-link11,flat-link12,flat-link13,flat-boxright1,flat-boxright2,flat-boxright3,flat-boxright4,flat-boxright5,flat-boxright6,flat-boxright9,flat-boxright10,flat-config/kwrd=SEGG+BETA2+POZNAN/async=1/kvcity=POZNAN/IV=201309162326510007913073/csr.js?AC=13d1c5237779b317&callback=onetShowAsynchAds @ 4
21:26:52.348 eval'ed code: link13spons = {
        "link": "Panele pod&#322;ogowe 31,50 z&#322;/m2. Zobacz", 
        "url": "http://fa4.clk.onet.pl/adclick/CID=102119/CCID=5399(...)
```

```
First css received in 1131 ms: <http://ir.ebaystatic.com/z/m2/0tqxqnqe2y2xzdar5mv4zhkd2.css>
First image received in 1290 ms: <http://p.ebaystatic.com/aw/pics/globalheader/spr9.png>
First js received in 1307 ms: <http://gh.ebaystatic.com/header/js/rpt.min?combo=11&ds=3&siteid=0&rvr=138&h=24036>
Redirect: <http://srx.main.ebayrtm.com/rtm?RtmCmd&a=json&l=@@__@@__@@&g=28a4f3d81410a565e5e5dcf5ffded58f&c=1H4sIAAAAAAAAACWNQQuCQBSE7%2F6KhS4V9Jz31tbVeOcgCIQ6FHTRChJKFzKsf5%2FWZYaZYfgm27Yxu2sw7AwnuSAHm%2FV2v0CaA0bANgrWQsOtbLr2UT5jkCM20%2BJfbHYxU0ayMve6eb2NS6q6mw0f7xRRYBn0XF%2FU%2BtMLAEdBbKKLwdlbFSzh8AusmcfIEr11XTjlcdz3PV2r8kPn9jEurAzyKXHmSJYyQlINRXE83JN59AVjhi39ywAAAA%3D%3D&p=11527:11528:11529:11530&di=11527:11528:11529:11530&v=4&enc=UTF-8&bm=401804&ord=1379366402040&cg=1379366402040&cb=$.billboard.callback&callback=jQuery1704923024866729975_1379366401938&_=1379366402042> is a redirect (HTTP 302)
(...)
Requests per domain:
 ir.ebaystatic.com: 2 request(s)
 www.ebay.com: 1 request(s)
 p.ebaystatic.com: 33 request(s)
 gh.ebaystatic.com: 2 request(s)
 thumbs.ebaystatic.com: 30 request(s)
(...)
JavaScript globals (34): $, $load, $radd, $rget, $rset, $rwidgets, $trk, $uri, GH, GH_config, Handlebars, Lens, _GlobalNavHeaderSrcPageId, activateSearch, buildFallback, cfg, checkLoginStatus, define, ebay, fmttime, functionType, handlebars, jQuery, jQuery1704923024866729975, loaded, max, openWindow, ppaOverlay, raptor, require, tick, toString, updateSignInLinkWithAction, vjo

The smallest response (0.00 kB): <http://rtm.ebaystatic.com/0/RTMS/Image/EDCO-eBP_Awareness_Q312-Refresh0928_shieldRightGlow_dkGreyBkgd-760x270.jpg>
The biggest response (85.29 kB): <http://www.ebay.com/>

The fastest response (14 ms): <http://rtm.ebaystatic.com/0/RTMS/Image/EDCO-eBP_Awareness_Q312-Refresh0928_shieldRightGlow_dkGreyBkgd-760x270.jpg>
The slowest response (5117 ms): <http://ebay-stories.com/wp-content/uploads/2013/09/lucky-380.jpg>

<http://rtm.ebaystatic.com/0/RTMS/Image/EDCO-eBP_Awareness_Q312-Refresh0928_shieldRightGlow_dkGreyBkgd-760x270.jpg> requested multiple times
Time spent on backend / frontend: 14% / 86%
```

## For developers

* [Project's wiki](https://github.com/macbre/phantomas/wiki)
* Description of [events fired by phantomas core](https://github.com/macbre/phantomas/wiki/Events)
* Description of [helper functions available to the browser in window.__phantomas](https://github.com/macbre/phantomas/wiki/Phantomas-scope)

## Utilities

* [CSS analyzer](https://github.com/macbre/phantomas/wiki/CSS-analyzer)
