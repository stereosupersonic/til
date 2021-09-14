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

## with ab - Apache HTTP server benchmarking tool

https://miceportal.com/moments?show_map=true&query=leonardohotels


```
ab -n 1000 -c 100 <website>

# This tests the site 1000 times in blocks of 100 times each.
```

result

```
Time taken for tests:   18.413 seconds
Complete requests:      1000
Failed requests:        0
Requests per second:    54.31 [#/sec] (mean)
````

If we can handle 50 requests a second that means we can handle 4.2 million requests a day.

https://stackoverflow.com/questions/12732182/ab-load-testing



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
