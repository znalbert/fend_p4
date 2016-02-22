## Website Performance Optimization portfolio project

###Part 1: Optimize PageSpeed Insights score for index.html

1. Refactored the directories into a src/ and dist/ structure.
1. Gulpfile.js copies files worked on in the src directory and processes them such that:
  * HTML, CSS, images, and JavaScript get copied to the dist/ directories after being linted.
  * JavaScript files are concatenated and the result is uglified.
  * Images get compressed.
  * CSS gets minified after having the last 2 most recent browser prefixes automatically inserted as appropriate.
  * HTML gets minified after having CSS inlined.
1. To get this up and running you just have to download the project, get the project dependencies with `npm install`, and then just run `gulp` and it'll be served with browserSync with in conjunction with `ngrok http 3000` I was able to get pagespeed insights scores of 96 for mobile and 97 for desktop. (However, browserSync caused hours of frustration on part 2 because I wasn't aware that it would show up in devtools as causing forced reflow, leading me to try to debug code that didn't need it. I ended up using `python -m SimpleHTTPServer` instead for that part.)


###Part 2: Optimize Frames per Second in pizza.html

1. Updated changePissaSizes() such that it no longer needed the determinedDx function. Then proceeded to address the forced synchronous layout by removing calculations that could be done outside of its `for` loop.
2. Updated updatePosition() in similar fashion by moving what I could outside of the `for` loop so that calculating the scroll from the top was done once and not for every pizza on every scroll. Also updated the CSS for the `.moving` class with `will-change: tranform` so as to move more of the processing to layer and composite as opposed to paint.
