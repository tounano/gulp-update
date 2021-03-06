# gulp-update

Incremental Npm update when package.json changes

This is a stateful stream. It never ends, because it should keep track of the `diffs` on package.json.

Make sure to create only one instance of it in your gulpfile.js.

## Under the hood

1. The first time it gets a package.json file, it will run an `npm install` command.
2. Afterwards, it will run install/remove only the new packages.

It can keep track of several package.json files.

## Usage:

The following example invokes an update with the `stream.write` api, however you can pipe other streams to
it as well.

The thing is that most of the streams would `end` as soon as they done, which will cause `gulp-update` to end as
well.

Simply make sure that the stream the is being piped to `gulp-update` won't end.

```js
var gulp  = require('gulp');

gulp.task('npmUpdate', function () {
  var update = require('gulp-update)();

  gulp.watch('./package.json').on('change', function (file) {
    update.write(file);
  });

})

gulp.task('default', ['npmUpdate']);
```

## install

With [npm](https://npmjs.org) do:

```
npm install gulp-update
```

## license

MIT
