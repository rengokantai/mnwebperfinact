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
The amount of time between the instant the user makes a request to the time the response arrives is known as Time to First Byte (TTFB).

