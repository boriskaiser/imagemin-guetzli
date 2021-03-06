# imagemin-guetzli [![Build Status](https://travis-ci.org/bradbaris/imagemin-guetzli.svg?branch=master)](https://travis-ci.org/bradbaris/imagemin-guetzli) [![Build status](https://ci.appveyor.com/api/projects/status/7wxmyhxee0i8b7d9/branch/master?svg=true)](https://ci.appveyor.com/project/bradbaris/imagemin-guetzli)

> [Guetzli](https://github.com/google/guetzli) imagemin plugin


## Install

```
$ npm install --save imagemin-guetzli
```


## Usage

```js
const imagemin = require('imagemin');
const imageminGuetzli = require('imagemin-guetzli');

imagemin(['images/*.{png,jpg}'], 'build/images', {
    use: [
        imageminGuetzli({quality: 95})
    ]
}).then(() => {
    console.log('Images optimized');
});
```

## Usage (gulp-imagemin):

```js
const gulp = require('gulp');
const imagemin = require('gulp-imagemin');
const imageminGuetzli = require('imagemin-guetzli');

gulp.task('default', () =>
    gulp.src('images/*')
        .pipe(imagemin([imageminGuetzli()]))
        .pipe(gulp.dest('dist/images'))
);
```

###Notes:
Guetzli is designed to work on high quality images (e.g. that haven't
been already compressed with other JPEG encoders). While it will work on other
images too, results will be poorer. You can try compressing an enclosed [sample
high quality
image](https://github.com/google/guetzli/releases/download/v0/bees.png).

Guetzli converts PNG/JPG to JPG. When using this plugin or guetzli-bin CLI, the original filename+ext is used as the output, although the image format has changed. You have to rename the file with the correct file extension (JPG) yourself afterwards.

## API

### imageminGuetzli([options])(buffer)

#### options

Type: `object`

##### quality

Type: `number` (0–100)<br>
Default: `95`

Set quality in units equivalent to libjpeg quality. As per guetzli function and purpose, it is not recommended to go below `84`.

Please note that JPEG images do not support alpha channel (transparency). If the input is a PNG with an alpha channel, it will be overlaid on black background before encoding.


## License

MIT © [imagemin](https://github.com/imagemin)

Much original code structure borrowed from imagemin-zopfli maintainers: [@kevva](https://github.com/kevva) [@sindresorhus](https://github.com/sindresorhus) [@shinnn](https://github.com/shinnn)