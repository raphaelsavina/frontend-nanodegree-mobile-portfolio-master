#Website Performance Optimization portfolio project

1. To view the page on a local web server:
  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

2. Open a browser and visit localhost:8080
3. Download and install [ngrok](https://ngrok.com/) to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ngrok http 8080
  ```

4. Copy the public URL ngrok gives you and test it through [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/) and [WebPageTest](http://www.webpagetest.org/).

#Work done:

##index.html
###Starting point:
PageSpeed Mobile: 28
PageSpeed Desktop: 30
Webpagetest 3G: fully loaded 15s

1. Optimised pizzeria.jpg from 1 very large 2Mb to 2 images: one 293px w and one 720px w (based on their used in pizza.html)
2. used pizza_293.jpg in index.html
3. Moved Google Analytics script (inline and linked) at the end of html.
4. Moved content of print.css into style.css to reduce number of calls. Will be ignore by media queries.
5. Removed loading of analystics.js. Could not see if it was used (seems duplicate of  inline script).
6. Removed Google font line as it seems to take way to long to load and is blocking rendering.
7. Optimized (ImagOptim) /img/profilepic.jpg. Also downloaded thumbnails and serving from /img to be sure they are fully optimised.
8. Minified css.
9. Optimize CSS Delivery as per https://developers.google.com/speed/docs/insights/OptimizeCSSDelivery
10. Minified HTML

###Results:
PageSpeed Mobile: 94
PageSpeed Desktop: 91
Webpagetest 3G: fully Loaded 2.3s

##pizza.html
###Starting point (from source):
	2015-12-13 17:06:17.681 main.js:494 Average time to generate last 10 frames: 49.501000000000204ms
	2015-12-13 17:06:18.444 main.js:494 Average time to generate last 10 frames: 46.564500000000045ms
	2015-12-13 17:06:20.018 main.js:466 Time to resize pizzas: 113.5649999999996ms
	2015-12-13 17:06:21.284 main.js:466 Time to resize pizzas: 113.5649999999996ms

1. Optimise pizzeria images, serving 2 versions media queries.
2. Work on updatePositions:
a. move "document.body.scrollTop / 1250" out of the for loop
b. added will-change: transform; to .main in style.css
c. changed left to transformX
d. No need to transform 200 pizzas, so get numbers of cols and rows to have the minimum visible requirement.
e. for resize pizza, no need to calc dx & newwidth in the for loop, all same size so getting these from [0] is enough

###Results:
	2015-12-13 17:07:10.162 main.js:496 Average time to generate last 10 frames: 0.3145000000018626ms
	2015-12-13 17:07:10.409 main.js:496 Average time to generate last 10 frames: 0.4790000000037253ms
	2015-12-13 17:07:12.541 main.js:468 Time to resize pizzas: 4.330000000009022ms
	2015-12-13 17:07:13.695 main.js:468 Time to resize pizzas: 4.330000000009022ms
	2015-12-13 17:07:16.534 main.js:496 Average time to generate last 10 frames: 0.37499999999854483ms


