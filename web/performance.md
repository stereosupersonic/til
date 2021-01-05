# Web Performance

https://github.com/davidsonfellipe/awesome-wpo

## Read

* https://csswizardry.com/2013/01/front-end-performance-for-web-designers-and-front-end-developers/

## Test the speed

* [Lighthouse](https://developers.google.com/web/tools/lighthouse/)
* [https://www.webpagetest.org/](https://www.webpagetest.org/)
* [google pagespeed](https://developers.google.com/speed/pagespeed/insights/)
* [yellowlab tools](https://yellowlab.tools/)

### local with docker

https://www.sitespeed.io/

```
docker run --rm -v "$(pwd):/sitespeed.io" sitespeedio/sitespeed.io:16.1.0 https://www.wartenberger.de
```

## Steps

### reduce assets size

#### images

* jpegoptim - shrinks size and removes meta data

```
  jpegoptim -0 -m75 --strip-all --all-progressive *.jpeg
```

* optipng - for PNG

#### remove unsed code

* css

* js



### caching and lazy loading
