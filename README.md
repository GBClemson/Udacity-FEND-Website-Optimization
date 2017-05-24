## Website Performance Optimization portfolio project

### How to Access the site:
1. go to my [Github](https://github.com/GBClemson/Udacity-FEND-Website-Optimization) repository for the project
2. In there you will see this readme, two folders and a super simple website that links to the original and final projects.
  * One folder named "src" contains the original files and images that I was assigned for the project
  * Other folder named "dist" contains the final files that I have edited with some comments showing some the changes that were made.
  * The site is also being hosted by github at: https://gbclemson.github.io/Udacity-FEND-Website-Optimization/

### Part 1: Optimize PageSpeed Insights score for index.html

#### Part 1 - Changes Made by Greg Bopp to index.html

1. Downloaded all image assets to utilize locally
2. Resized and compressed all images.
3. Used local fonts vs remote fonts.
4. Brought all css to index.html to avoid linking to other files.
5. Placed above the fold CSS in my header and placed other CSS below the body.
6. added an .htaccess file to the server to leverage browser caching.
7. Placed the links for analytics.js and perfmatters.js below the body.

### Part 2: Optimize Frames per Second in pizza.html

#### Part 2 - Changes Made by Greg Bopp to pizza.html
1. Moved #movingPizzas1 above the header content and gave it: class="col-md-12" so it is not reconfiguring on window resize
2. Compressed pizzeria image from 2315kb down to 25kb
3. Simplified / minimized the nav button code
4. Removed unnecessary entries from style.css.
5. Utilized bootstrap classes for centering text and sizing columns.
6. Moved style.css to pizza.html for Google Page Speed boost.
7. Set a pixel width for the elements that make up a random pizza entry. This allows for a very simple width change on the pizza image to convey the correct size of the pizza. This allowed the resizePizza function to be dramatically simplified.

#### Part 2 - Steps taken by Greg Bopp to de-jankify main.js
1. Scaled down and compressed pizza.png. Scaled down to 77x100px since that is the size of the background pizzas. Used http://compresspng.com/ to compress the original size of the pizza.png image from 49kb to 5kb.
2. Reduced the number of bg pizzas being generated from 200 to 24. Realigned the vertical positions to match the users display. No need to have more than 3 rows of random flying pizza on a screen at a time.
3. Removed the "updatePostions" inside of: document.addEventListener('DOMContentLoaded', function() {
4. Made the updatePositions function more efficient by simplifying / changing the following code:
    * Chanaged className  to classList.
    * Utilized requestAnimationFrame to only update the pizza positions when we can and not with every scroll / mouse down event.
    * Utilized style.transform and translateX to update the Xpos of the sliding pizza bg.
      * This required a simple update in pizza.html where the #movingPizzas1 div was changed to col-md-12 and it is not inside of a row.
5. Made efficiency improvements to the pizza slider and random generated pizzas:
    * Simplified the determineDx function. ignoring the windowWdth, simplified the sizes to just be 3 fixed sizes when the pizza slider is used.
    * Did away with the percentages in sizeSwitcher and simplified the math. Now it is just a simple subtract the old width from the new width and then apply the changes to all of the random pizza pics.
    * Completely removed the use of "document.querySelectorAll(".randomPizzaContainer")" calls by utilizing getElementsByClassName and querySelector.
    * Created a variable named numOfPizzas to store the correct number of random pizzas generated.
    * Took as much math out of the changePizzaSizes for loop as possible. It is now just one line that applies the size changes to each of the random pizza entries.
6. Went back into resizePizzas function and made more dramatic simplification to the pizza slider calculations:
    * Completely did away with determineDx and just used the slider to generate a new width for the pizza.png image. This method allows us to completely ignore the old size and just make each element the new size based on the slider position.

## Original Readme contents:

Your challenge, if you wish to accept it (and we sure hope you will), is to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques you've picked up in the [Critical Rendering Path course](https://www.udacity.com/course/ud884).

To get started, check out the repository and inspect the code.

### Getting started

#### Part 1: Optimize PageSpeed Insights score for index.html

Some useful tips to help you get started:

1. Check out the repository
1. To inspect the site on your phone, you can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

1. Open a browser and visit localhost:8080
1. Download and install [ngrok](https://ngrok.com/) to the top-level of your project directory to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ./ngrok http 8080
  ```

1. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! Optional: [More on integrating ngrok, Grunt and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)

Profile, optimize, measure... and then lather, rinse, and repeat. Good luck!

#### Part 2: Optimize Frames per Second in pizza.html

To optimize views/pizza.html, you will need to modify views/js/main.js until your frames per second rate is 60 fps or higher. You will find instructive comments in main.js.

You might find the FPS Counter/HUD Display useful in Chrome developer tools described here: [Chrome Dev Tools tips-and-tricks](https://developer.chrome.com/devtools/docs/tips-and-tricks).

### Optimization Tips and Tricks
* [Optimizing Performance](https://developers.google.com/web/fundamentals/performance/ "web performance")
* [Analyzing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/analyzing-crp.html "analyzing crp")
* [Optimizing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path.html "optimize the crp!")
* [Avoiding Rendering Blocking CSS](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css.html "render blocking css")
* [Optimizing JavaScript](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript.html "javascript")
* [Measuring with Navigation Timing](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/measure-crp.html "nav timing api"). We didn't cover the Navigation Timing API in the first two lessons but it's an incredibly useful tool for automated page profiling. I highly recommend reading.
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/eliminate-downloads.html">The fewer the downloads, the better</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html">Reduce the size of text</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization.html">Optimize images</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching.html">HTTP caching</a>

### Customization with Bootstrap
The portfolio was built on Twitter's <a href="http://getbootstrap.com/">Bootstrap</a> framework. All custom styles are in `dist/css/portfolio.css` in the portfolio repo.

* <a href="http://getbootstrap.com/css/">Bootstrap's CSS Classes</a>
* <a href="http://getbootstrap.com/components/">Bootstrap's Components</a>
