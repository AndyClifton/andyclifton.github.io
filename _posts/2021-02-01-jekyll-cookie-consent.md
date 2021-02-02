---
title: 'How to implement a cookie consent banner for a jekyll website'
date: 2021-02-01
draft: false
excerpt: Cookie consent banners are legally required, but not often included in Jekyll website templates. Here's how you do it.
featured-image: /images/2021/02/sara-sperry--EMvlQ5n8n0-unsplash.jpg
permalink: /posts/2021/02/jekyll-cookie-consent/
tags:
  - software development
---

As a result of the [EU's GDPR legislation and the ePrivacy Directive](https://consent.guide/google-analytics-cookie-consent/), websites that are accessible in the EU are required to allow the users to control what information is gathered about them, and how this is used. The most obvious result of this are the cookie consent banners that you have to approve when you visit most websites for the first time. Unfortunately those banners are not a standard Jekyll feature, so you'll have to make your own.

There are a couple of steps we need to go through.
1. Creating the cookie banner itself
2. Linking the "accept" button on the banner to google analytics
3. Avoid counting page views during development

## Implementing a cookie consent banner in Jekyll
This is pretty easy once you know how! There is some very good code by Joost van der Schee available from [the Jekyll Codex](https://jekyllcodex.org/without-plugin/cookie-consent/), which can be used freely ([according to the site license](https://jekyllcodex.org/about)).  

It's a file - _cookie-consent.html_ - that you should save in your __includes/_ directory, and include towards the bottom of you default HTML layout, like this:

````
...
{ % include cookie-consent.html % }
</body>
</html>
```` 

(note that usually you would write `{ %` and `% }` __without spaces between the % and } symbols__ but this causes trouble here!)


The cookie consent banner code in _cookie-consent.html_ includes this crucial code:

````    
if(readCookie('cookie-notice-dismissed')=='true') {
    { % include ga.js % }
    { % include chatbutton.js % }
} else {
    document.getElementById('cookie-notice').style.display = 'block';
}
````

This means that once you have the user's consent, you can run whatever javascript you need. You can edit the ````{ % include blah.js % }```` to call whatever files you want.

## Adding Google Analytics
Our next step is to call the javascript that passes the information about page views back to Google. This is implemented in the _ga.js_ script that is included in _cookie-consent.html_.

### Get a tracking code
We'll need a google analytics tracking code. You can get this from [analytics.google.com](https://analytics.google.com). I'll not go into details, but the short version is that you want a code for a website.

Then we'll add this to our site's __config.yml_ file so that we can call it by reference, elsewhere:

````
google_analytics_id: G-ABCDEFGH
````

### The javascript
Now we need to create a file called _/includes/ga.js_, which is where we'll store the actual code we want to run.

I picked up this code from [Coralie Collignon's blog](https://www.coraliecollignon.com/jekyll/2020/10/22/google-analytics.html), who in turn acknowledges to having picked it up from [Stack Overflow](https://stackoverflow.com/questions/51833090/put-google-analytics-code-in-an-js-file/51833302). Anyway, put it all in your new _/includes/ga.js_ file.

````
/*This function will load script and call the callback once the script has loaded*/
function loadScriptAsync(scriptSrc, callback) {
    if (typeof callback !== 'function') {
        throw new Error('Not a valid callback for async script load');
    }
    var script = document.createElement('script');
    script.onload = callback;
    script.src = scriptSrc;
    document.head.appendChild(script);
}

/* This is the part where you call the above defined function and "call back" your code which gets executed after the script has loaded */
loadScriptAsync('https://www.googletagmanager.com/gtag/js?id={#YOUR-TRACKING-ID}', function(){
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());
    gtag('config', '{#YOUR-TRACKING-ID}', { 'anonymize_ip': true });
})
````

This should all work. You can check it works using [cookiebot](https://www.cookiebot.com/en/).

## How to avoid recording your development clicks
You can set flags in your code to detect which environment you are in - development, production, or whatever. There's more about this on the [Jekyll home page](https://jekyllrb.com/docs/configuration/environments/).

### Using Github pages
GitHub Pages sets ```JEKYLL_ENV``` to ```production``` automatically when you push Jekyll source code to GitHub build it using pages. This means that you have access to a variable, ```jekyll.environment == "production"``.`

Then you can modify _cookie-consent.html_ to detect that flag, and only call google analytics when you are in your production environment:

````
if(readCookie('cookie-notice-dismissed')=='true') {
    { % if jekyll.environment == "production" and site.google_analytics_id % }
        { % include google-analytics.js % }
    { % endif % }
}
````

_et voila_! Now you will only get "production" traffic showing up in your analytics.

### Using other build services
There are similar approaches you can use in Heroku and other build services as well. For example, I build another site through netlify. There I set the environment variable in my __netlify.toml_ file:

````
[build.environment]
  JEKYLL_ENV = "production"
````

## More complex consent
In this example I'm asking for consent for one set of data transfer to Google Analytics. This is the only consent I need for my website. in other cases it might be necessary to implement a more extended set of buttons to request permission for advertising, using facebook "like" services, or for comments. You'll probably need a different approach for that. 

## All done
Here I've shared how I implement a simple consent banner for a jekyll website that requests permission to collect and use data through google analytics. I hope this helps!