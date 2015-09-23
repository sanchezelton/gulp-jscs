# gulp-jscs [![Build Status](https://travis-ci.org/jscs-dev/gulp-jscs.svg?branch=master)](https://travis-ci.org/jscs-dev/gulp-jscs)

> Check JavaScript code style with [JSCS](http://jscs.info)

![](screenshot.png)

*Issues with the output should be reported on the JSCS [issue tracker](https://github.com/jscs-dev/node-jscs/issues).*


## Install

```
$ npm install --save-dev gulp-jscs
```


## Usage

### Reporting

```js
const gulp = require('gulp');
const jscs = require('gulp-jscs');

gulp.task('default', () => {
	return gulp.src('src/app.js')
		.pipe(jscs())
		.pipe(jscs.reporter());
});
```

### Fixing

```js
const gulp = require('gulp');
const jscs = require('gulp-jscs');

gulp.task('default', () => {
	return gulp.src('src/app.js')
		.pipe(jscs({fix: true}))
		.pipe(gulp.dest('src'));
});
```


## Results

A `jscs` object will be attached to the file object which can be used for custom error reporting. An example with one error might look like this:

```js
{
	success: false,  // or true if no errors
	errorCount: 1,   // number of errors in the errors array
	errors: [{       // an array of jscs error objects
		filename: 'index.js',  // basename of the file
		rule: 'requireCamelCaseOrUpperCaseIdentifiers',  // the rule which triggered the error
		message: 'All identifiers must be camelCase or UPPER_CASE',  // error message
		line: 32,  // error line number
		column: 7  // error column
	}]
};
```


## API

### jscs([options])

#### options

See the JSCS [options](http://jscs.info/overview.html#options).

Alternatively you can set the `configPath` *(default: `'.jscsrc'`)* option to the path of a [.jscsrc](http://jscs.info/rules.html) file.

Set `fix: true` if you want jscs to attempt to auto-fix your files. Be sure to pipe to `gulp.dest` if you use this option.

### jscs.reporter([reporter])

See the JSCS [reporter docs](http://jscs.info/overview#-reporter-r) for supported input.

This plugin also ships with some custom reporters:

- `fail` - Emits an error at the end of the stream if there are lint errors.
- `failImmediately` - Emits an error immediately if there are lint errors.


## License

MIT © [Sindre Sorhus](http://sindresorhus.com)
