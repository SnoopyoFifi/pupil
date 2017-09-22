# API

- `package.json`

```json

  {
    "name": "gulp-demo",
    "version": "1.0.0",
    "description": "",
    "main": "gulpfile.js",
    "devDependencies": {
      "gulp": "^3.9.1",
      "gulp-concat": "^2.6.1",
      "gulp-debug": "^3.1.0",
      "gulp-imagemin": "^3.2.0",
      "gulp-less": "^3.3.2",
      "gulp-load-plugins": "^1.5.0",
      "gulp-minify-css": "^1.2.4",
      "gulp-minify-html": "^1.0.6",
      "gulp-uglify": "^2.0.1",
      "imagemin-pngquant": "^5.0.0",
      "jquery": "^3.2.1",
      "jszip": "^3.1.3",
      "layui-layer": "^1.0.9",
      "run-sequence": "^1.2.2",
      "three": "^0.84.0"
    },
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": "gulp",
    "author": "Snoopy",
    "license": "ISC"
  }


```

- `gulpfile.js`

```js

  var gulp = require('gulp'),
    sequence = require('run-sequence'),
    pngquant = require('imagemin-pngquant'),
    concat = require('gulp-concat'),
    less = require('gulp-less');

  var plugin = require('gulp-load-plugins')(gulp);

  gulp.task('default', ['build'], function(){
    return gulp.watch(['src/static/less/**', 'src/static/js/**'])
  });

  gulp.task('imagemin', function(){
    return gulp.src('src/static/img/**/*.*')
        .pipe(plugin.debug({title: 'imagemin'}))
        .pipe(plugin.imagemin({
          progressive: true,
          svgoPlugins: [{removeViewBox: false}],
          use: [pngquant()]
        }))
        .pipe(gulp.dest('dest/static/img'));
  });

  gulp.task('cssmin', function(){
    return gulp.src('src/static/css/**/*.css')
        .pipe(plugin.debug({title: 'jsmin'}))
        .pipe(plugin.uglify())
        .pipe(gulp.dest('dest/static/css'))
  });

  gulp.task('jsmin', function(){
    return gulp.src('src/static/js/**/*.js')
        .pipe(plugin.debug({title: 'jsmin'}))
        .pipe(plugin.uglify())
        .pipe(gulp.dest('dest/static/js'))
  });

  gulp.task('font', function(){
    return gulp.src('src/static/fonts/**')
        .pipe(plugin.debug({title: 'fonts'}))
        .pipe(gulp.dest('dest/static/fonts'))
  });

  gulp.task('concat', function(){
    return gulp.src('src/static/js/**/*.js')
        .pipe(concat('all.js'))
        .pipe(gulp.dest('dest/static/js'))
  })

  gulp.task('less', function(){
    return gulp.src('src/static/less/**/*.less')
        .pipe(less())
        .pipe(gulp.dest('dest/static/css'))
  })

  gulp.task('build', function (done) {
     sequence('imagemin', 'less', 'cssmin', 'concat', 'jsmin', 'font', done);
  });


```
