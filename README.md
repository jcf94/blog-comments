# blog-comments

A repository for my personal blog.

# To initialize all my posts, I used Tempermonkey script

First script to open the posts

```javascript
// ==UserScript==
// @name         Open posts from archives
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  try to take over the world!
// @author       You
// @match        http://jcf94.com/archives/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
    var list = $(".post-title-link");
    console.log(list.length + " items get");
    for (let i=0;i<list.length;i++)
        window.open(list[i].href);
    // Your code here...
})();
```

Second script to do the initialization

```javascript
// ==UserScript==
// @name         Init
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  try to take over the world!
// @author       You
// @match        http://jcf94.com/*
// @grant        window.close
// ==/UserScript==

function fireMouseEvents( query, eventNames ){
    var element = document.querySelector(query);
    if(element && eventNames && eventNames.length){
        for(var index in eventNames){
            var eventName = eventNames[index];
            if(element.fireEvent ){
                element.fireEvent( 'on' + eventName );
            } else {
                var eventObject = document.createEvent( 'MouseEvents' );
                eventObject.initEvent( eventName, true, false );
                element.dispatchEvent(eventObject);
            }
        }
    }
}

(function() {
    'use strict';
    //fireMouseEvents("a[href*='/archives/']",['mouseover','mousedown','mouseup','click']);

    if (document.readyState == "complete" || document.readyState == "loaded" || document.readyState == "interactive") {
        console.log("Already Loaded");
    } else {
        document.addEventListener("DOMContentLoaded", function(event) {
            console.log("Just Loaded");
        });
    }

    let init = $(".gitment-comments-init-btn");

        setTimeout(function() {
            init = $(".gitment-comments-init-btn");
            if (init.length > 0)
            {
                console.log("Init Button Get.");
                fireMouseEvents(".gitment-comments-init-btn",['mouseover','mousedown','mouseup','click']);
                setTimeout(function(){
                    window.close();
                }, 10000);
            }
            else console.log("Init Button Not Found.");
        }, 10000);

    // Your code here...
})();
```
