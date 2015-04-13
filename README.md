# Wiredep-
Gulp task for auto-linking all .js/.css/.etc dependencies inside index.html



'use strict';

var gulp    = require('gulp'),
    wiredep = require('wiredep').stream;

gulp.task('wiredep', function () {
  return gulp.src('./client/index.html')
    .pipe(wiredep({
      directory: './bower_components',
      bowerJson: require('../bower.json'),
      fileTypes: {
        html: {
          replace: {
            js: function (filePath) {
              return '<script src="bower_components/' +
                filePath.split('/').pop() + '"></script>';
            },
            css: function (filePath) {
              return '<link rel="stylesheet" href="bower_components/' +
                filePath.split('/').pop() + '" />';
            }
          }
        }
      }
    }))
    .pipe(gulp.dest('./dist'));
});
