# gulp-tslint-jenkins-reporter
gulp-tslint checkstyle reporter, to be used by Jenkins (Hudson). Writes output to an xml file.

## Install
```bash
npm install gulp-tslint-jenkins-reporter -D
```

## Usage
```javascript
var gulp = require('gulp');
var tslint = require('gulp-tslint');
var tslintReporter = require('gulp-tslint-jenkins-reporter');

gulp.task('lint', function() {
    return gulp.src('./src/*.ts')
        .pipe(tslint())
        .pipe(tslintReporter());
});
```

## Advanced usage
```javascript
var gulp = require('gulp');
var tslint = require('gulp-tslint');
var tslintReporter = require('gulp-tslint-jenkins-reporter');

gulp.task('lint', function() {
    return gulp.src('./src/*.ts')
        .pipe(tslint())
        .pipe(tslintReporter({
            sort: true,
            filename: 'checkstyle.xml',
            severity: 'error',
            pathBase: '/project',
            pathPrefix: ''
        }));
});
```

## Options

**sort**
type: `boolean`
default: `false`
will sort the files alphabetically within the report using their path.

**filename**
type: `string`
default: `checkstyle.xml`
the filename to write the report. Works with a path as well, missing directories will be created.

**severity**
type: `string`
default: `warning`
values: `error`|`warning`|`info`
Since version 5.0, tslint does provide a severity field.
This option will be kept for backward compatibility and act as a default value for failures without severity.

**pathBase**
type: `string`
default: `''`
If given, the path of the files will be rebased according to the value. For instance, if your file path is
```
/my/awesome/yet/too/long/path/for/my/file.ts
```
and that you set
```javascript
{
    pathBase: '/path/for/my'
}
```
you will end up with
```
/my/file.ts
```

**pathPrefix**
type: `string`
default: `''`
a prefix to add to the path. Given the previous example, you could also add this :
```javascript
{
    pathBase: '/path/for/my',
    pathPrefix: '/src'
}
```
and end up with
```
/src/file.ts
```

## LICENSE

The MIT License (MIT)
