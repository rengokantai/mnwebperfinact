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
