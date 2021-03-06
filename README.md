# mnwebperfinact
##1 Understanding web performance
####1.1.2. How web browsers talk to web servers
In communication between HTTP/1 servers and browsers, a phenomenon known as __head-of-line blocking__ can occur.    
This occurs because the browser limits the number of requests it will make at a single time (typically, six).  

####1.1.3. How web pages load

###1.2. Getting up and running
####1.2.3. Simulating a network connection
click the Network tab, check Disable cache, in drop-down menu labeled No throttling, select the Regular 3G profile.

###1.3. Auditing the client’s website

###1.4. Optimizing the client’s website
using toy minifier
```
npm install –g minifier html-minify
```
minify css
```
minify -o styles.min.css styles.css
minify -o jquery.min.js jquery.js
```
####1.4.2. Using server compression
request: 
```
GET /index.html
Accept-Encoding:gzip,deflate
```
response:
```
Content-Encoding:gzip
```

install npm conpression package
```
npm install compression --save
```
in app.js
```
var compression = require("compression");
app.use(compression());
```

for apache
```
<IfModule mod_deflate.c>
  AddOutputFilterByType DEFLATE text/html text/css text/javascript;
</IfModule>
```
__Avoid compressing file types that already use compression when they’re encoded, such as JPEG, PNG, and GIF images and WOFF and WOFF2 font files.__
####1.4.3. Optimizing images
[tinypng](http://tinypng.com)



##2. Using assessment tools
###2.1. Evaluating with Google PageSpeed Insights
[google insights](https://developers.google.com/speed/pagespeed/insights/)

####2.1.2. Using Google Analytics for bulk reporting

###2.3. Inspecting network requests
####2.3.1. Viewing timing information
The amount of time between the instant the user makes a request to the time
the response arrives is known as Time to First Byte (TTFB).  


Prior to the request being made, a few steps occur, such as queueing the request,
DNS lookup, connection setup, and the SSL handshake.
######A note on DNS lookups
In Chrome, you can look at the DNS cache by going to [here](chrome://netinternals#dns)


###2.4. Rendering performance-auditing tools
####2.4.1. Understanding how browsers render web pages
steps:
- Parse HTML to create the Document Object Model (DOM)—When the HTML is downloaded from the web server, it’s parsed by the browser to build the DOM, which is a hierarchical representation of the HTML document’s structure.
- Parse CSS to create the CSS Object Model (CSSOM)—After the DOM is built, the browser parses the CSS and creates the CSSOM. This is similar to the DOM, except it represents the way that CSS rules are applied to the document.
- Lay out elements—The DOM and CSSOM trees are combined to create a render tree. The render tree then goes through the layout process, where CSS rules are applied and elements are laid out on the page to create the UI.
- Paint page—After the document has finished the layout process, the cosmetic aspects of the page are applied from the CSS and media in the page. At the end of the painting process, the output is converted into pixels (rasterized) and displayed on the screen.


####2.4.2. Using Google Chrome’s Timeline tool
- Loading (Blue)— Network-related events such as HTTP requests. It also includes activity such as the parsing of HTML, CSS, and image decoding.
- Scripting (Yellow)— JavaScript-related events. These can range from DOM-specific activity, to garbage collection, to site-specific JavaScript, and to other activity.
- Rendering (Purple)— Any and all events relating to page rendering. Events in this category are activities such as applying CSS to the page HTML, and events that cause re-rendering such as changes to the page’s HTML triggered by JavaScript.
- Painting (Green)— Events related to drawing the layout to the screen, such as layer compositing and rasterization.

####2.4.3. Identifying problem events: thy enemy is jank 
Janky frames
- review this.
CSS transitions are a technology native to CSS that are perfect for linear animations. __Because they’re built into the browser__, they also have none of the overhead of jQuery, and can perform better than timer-based animations that use setTimeout and setInterval, such as jQuery’s animate method.  

Difference between top and transformY
- Rather than use the top property to position the element, you’ve changed this to a transform property by using the translateY method. Like the top property, this transform method repositions the element on the y-axis. __The difference, though, is that transforms animate better, and with less jank__, which is what you’re after.





###2.5. Benchmarking JavaScript in Chrome
time,timeEnd with label
```
console.time("querySelector"); document.querySelector("#schedule"); console .timeEnd("querySelector");
```


####2.6.2. Debugging websites remotely on Android devices
####2.6.3. Debugging websites remotely on iOS devices

=================================

##3. Optimizing CSS
####3.1.3. Culling shallow selectors
remove all the unused CSS from the style sheet.
```
npm install -g uncss
uncss http://localhost:8080 -i .modal.open > css/styles.clean.css
```


####3.1.7. Finding redundancies with csscss
```
gem install csscss
csscss styles.css –v –-no-match-shorthand
```
The --no-match-shorthand argument keeps the program from expanding any matching shorthand rules such as border-bottom into more-explicit rules such as border-bottom-style. If you want to expand those rules, remove that switch.







##5. Making images responsive






















##7. Faster fonts
####7.1.2. Rolling your own @font-face cascade
|format|extension|support|
|---|---|---|
|Truetype   |ttf   |All except IE8 and below   |
|Embedded Open Type   |eot   |IE6+   |
|WOFF   |woff   |All except for Android Browser 4.3 and below and IE8 and below   |
|WOFF2  |woff2  | FF39+ chrome36+ Opera23+ Android 4.7+ |


some npm package
```
ttf2eot //Converts TTF to Embedded OpenType (EOT)
ttf2woff //Converts TTF to WOFF
ttf2woff2 //Converts TTF to WOFF2
```

```
npm install -g ttf2eot ttf2woff ttf2woff2
```



##8. Keeping JavaScript lean and fast
###8.1. Affecting script-loading behavior
####8.1.1. Placing the <script> element properly
Browsers read HTML documents from top to bottom. When links to external resources (such as scripts, in this case) are found, the browser stops to parse them. When parsing occurs, rendering is blocked.  

As this goes on, the browser puts the rendering of the page __on the back burner.__(postpone)  

To measure the __Time to First Paint__ for the client’s website, select the Regular 3G throttling profile to simulate page loading on a slower connection.  





####8.3.6. Using the Fetch API

###8.4. Animating with requestAnimationFrame


####8.4.5. Dropping in Velocity.js
with jQuery
```
$(".item").velocity({
    opacity: 1,
    left: 8px
}, 500);
```

without jQuery
```
Velocity(document.querySelector(".item"), {
    opacity: 1,
    left: 8px
}, {
    duration: 500
});
```



## 11. Looking to the future with HTTP/2
http/1 three issues:
- head-of-line blocking
- uncompressed headers
- nonsecure websites.  

###### Head-of-line blocking
One way to ameliorate this problem on the front end is to __bundle files__    
Another rather hacky way around this request limit is to use a technique called __domain sharding__

###### Uncompressed headers
__Server compression compresses only the body of the response, not its response headers.__


#### 11.1.2. Solving common HTTP/1 problems via HTTP/2


#### 11.1.4. Observing the benefits
```
chrome://net-internals#timeline
```


#### 11.3.2. Using Server Push
```
<Location /index.html>
    Header add Link: </css/styles.min.css>; rel=preload; as=style"
</Location>
```















##12. Automating optimization with gulp
```
/
src
 img
 js
 less
dist
```
install gulp4
```
npm show gulp version
npm install gulpjs/gulp#4.0 --save
```

###### Essential plugins
```
npm install gulp-util del gulp-livereload gulp-ext-replace gulp-htmlmin gulp-less gulp-postcss autoprefixer autorem cssnano --save
npm install gulp-uglify gulp-concat --save
npm install gulp-imagemin imagemin-webp imagemin-jpeg-recompress imagemin-pngquant imagemin-gifsicle imagemin-svgo --save
```





