# readability

Turn any web page into a clean view. It's based on arc90's readability project.

## Install

    npm install readability

## Usage

See examples folder for a complete example

## Read a web page

`readability.read(html [, options], callback)`

Where

  * **html** url or html code.
  * **options** is an optional options object
  * **callback** is the callback to run - `callback(error, read)`

Example

    var readability = require('./readability');

    // source file is iso-8859-15 but it is converted to utf-8 automatically
    readability.read('http://howtonode.org/really-simple-file-uploads', function(err, readResult) {
      console.log(readResult.getArticleContent());
    });

**NB** If the file has been marked with charset other than utf-8, it is converted automatically. Charsets such as GBK, GB2312 is also supported via icon.

## Options

Possible option values

 * **maxRedirects** how many redirects allowed, defaults to 10
 * **disableRedirects** set to true if redirects are not allowed, defaults to false
 * **headers** optional header fields, in the form of `{'Header-Field':'value'}`
 * **maxResponseLength** maximum allowed length for the file, the remainder is cut off. Defaults to `Infinity`
 * **method** defaults to GET
 * **payload** request body
 * **disableGzip** set to false, to disable content gzipping, needed for Node v0.5.9 which has buggy zlib
 * **cookies** an array of cookie definitions in the form of `['name=val']`
 * **cookieJar** for sharing cookies between requests, see below
 * **outputEncoding** 
 * **disableDecoding** set to true to disable automatic charset decoding to utf-8
 * **overrideCharset** set input encoding
 * **asyncDnsLoookup** use high performance asynchronous DNS resolution based on c-ares instead of a thread pool calling getaddrinfo(3)
 * **timeout** set a timeout in ms
 * **agent** pass-through http.request agent parameter

## readResult

Readability support lazy evaluation by passing `readResult` to the callback function.

### readResult.getArticleContent()

Return the article content of the web page. Return `false` if failed.

### readResult.getArticleTitle()

Return the article title of the web page.

### readResult.getHTML()

Return the original html source code.

### readResult.getDocument()

Return the document of the web page generated by jsdom.

## License

This code is under the Apache License 2.0.  http://www.apache.org/licenses/LICENSE-2.0