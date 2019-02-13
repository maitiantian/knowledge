# gulp

[gulp workdir template](https://github.com/maitiantian/work-with-gulp)

```javascript
// gulpfile.js
var gulp = require('gulp');
var browserSync = require('browser-sync').create();
var reload = browserSync.reload;

gulp.task('default', function(){
	browserSync.init({
		server: {
			baseDir: "./"
		}
	});

	gulp.watch("./index.html").on('change', reload);
	gulp.watch("./css/*.*").on('change', reload);
	gulp.watch("./js/*.*").on('change', reload);
});
```

```json
// package.json
{
  "name": "work-with-gulp",
  "version": "1.0.0",
  "description": "a standard gulp workdir",
  "main": "index.js",
  "devDependencies": {
    "browser-sync": "^2.24.7",
    "gulp": "^3.9.1"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "jquery": "git checkout c0afa3a ./src",
    "react": "git checkout 8a50481 ./src"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/maitiantian/work-with-gulp.git"
  },
  "keywords": [
    "gulp"
  ],
  "author": "maitiantian",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/maitiantian/work-with-gulp/issues"
  },
  "homepage": "https://github.com/maitiantian/work-with-gulp#readme"
}
```