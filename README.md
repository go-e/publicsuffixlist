PublicSuffixList
================

This module validates domain names and top level domains, making use of the
[Public Suffix List](http://www.publicsuffix.org) used in modern browsers like
Google Chrome, Mozilla Firefox and Opera.

## Installation

The module can be installed via npm or by cloning this repository manually.

```js
npm install publicsuffixlist
```

A current copy of Mozilla's Public Suffix List will be downloaded automatically
when npm is used.

After a manual installation, it is necessary to run the download_list.js script
in the root folder in order to download this list.

## Running the unit tests

Please download and install the [Mocha](http://mochajs.org) test framework
globally (you might have to have superuser rights):

```bash
npm install mocha -g
```

Then run the following command:

```bash
mocha spec
```

## Usage

```js
var PublicSuffixList = require('publicsuffixlist');

// Create a new PublicSuffixList instance
var psl = new PublicSuffixList(options);

psl.initialize(function (err) { // initialize psl asynchronously or
  // Use the methods described below
});

psl.initializeSync(); // initialize psl synchronously
// Use the methods described below

```

### Options

##### ``filename {string}``
Supplies a filename as source for the data file.
This will be Mozilla's "effective_tld_names.dat" by default.

##### ``buffer {object}``
Supplies a buffer as source for the data file.

##### ``lines {string[]}``
Supplies an array of strings as source for the data file.

### Initialization

##### ``.initialize(callback)``
Loads all rules from the specified source.

##### ``.initializeSync()``
Loads all rules synchronously from the specified source.

In order to use this module, it must be initialized synchronously or
asynchronously with a ruleset.
By default, the ruleset is loaded from disk.

### Methods

##### ``.lookup(domainString)``
lookup() returns an object providing the distinct results for the queried
string or null in case of an invalid query.

```js
var result = psl.lookup('www.domain.com');

/* result === { domain: 'domain',
              tld: 'com',
              subdomain: 'www' } */
```

##### ``.domain(domainString)``

Get the assignable domain from the fully qualified domain name.

```js
var result = psl.domain('www.domain.com');

/* result === 'domain.com' */
```

##### ``.validateTLD (tld)``

Validates the provided top level domain. Returns true or false.

```js
var validTLD = psl.validateTLD('de'); // true
var invalidTLD = psl.validateTLD('ed'); // false
```

##### ``.validate (domainString)``

Returns true when the provided domain is valid, otherwise false.

```js
var validDomain = psl.validate('domain.de'); // true
var invalidDomain = psl.validate('domain.yz'); // false
```

## Tests

Tests are included in the spec/ directory. In order to run these, you will need
to install the Mocha testing framework and execute the following command:

```bash
mocha spec
```

## Changes
0.2.3
+ correcting a rule lookup issue

0.2.2
+ Adding an initializeSync() method
+ fixed some typing and syntax errors

0.2.1
+ Loading Mozilla's public suffix list by default when nothing else was
  declared

0.2.0
+ Adding ability to load rules from buffers, files and arrays of rules
+ API change: removing .parse(), asynchronous initialization
+ adding .domain()
+ re-written unit tests
+ changing the publicsuffix list URL

0.1.31
+ adapting to current Node's API changes in order to remove the warning messages
+ updated tests
+ fixed some typing and syntax errors

0.1.3
+ added support for generic TLDs
+ added lookup() and validateTLD()

0.1.1, 0.1.2
+ Removed dependency on [Underscore.js](http://documentcloud.github.com/underscore/)
+ added support for automatic installation on the Windows platform

0.1.0
+ first release

Further reading
---------------
* [publicsuffix.org](http://www.publicsuffix.org)
* [Mozilla Wiki: Public Suffix List](https://wiki.mozilla.org/Public_Suffix_List)

Credits
-------

* [Kirill Dmitrenko](https://github.com/dmikis) added loading Mozilla's public
  suffix list by default (if nothing else was declared)
* [Morton Swimmer](https://github.com/mswimmer) forked this library, added
  a .domain() method and updated the URL of the list
* [Simone Carletti](http://www.simonecarletti.com/code/public_suffix_service/)
* domainname-parser.googlecode.com

License
-------

MIT License.
