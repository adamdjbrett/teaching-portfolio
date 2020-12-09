---
title: 'Step 4: Review your privacy settings 👀' 
date: 2020-11-20
permalink: /getting-started/step-four/index.html
eleventyNavigation:
  order: 18
  parent: Home
  key: Step 4 
  title: 'Step 4: Configure access'
---
By default, spacebook sites are set up so they will **NOT** get indexed by Google or other search engines. They do not send referrer links to outside sites and cannot be tracked in analytics. There are no ad trackers, tracking cookies, or other nonsense installed. 

If you want to open your site to the public eye, [jump down for easy instructions](#make-your-site-searchable!) on how to share your spacebook with Google and the rest of the world.


## Level 1: Security through obscurity

By default, your site is hidden from search engines and won't send referrer links but it is not truly secure. Anybody who discovers the link will be able to view the site. This is similar to the **Anyone with the link** permissions commonly set on Google Docs. You can use an obscured Netlify site URL for added protection against accidental discovery. This is the default setting and safe for many use cases. 

## Level 2: Encryption

If privacy is a priority and you wish to you put your site behind a password, you can do so by following the [password protection](/encryption) instructions. This will encrypt all of your files, and require all users to enter a password before viewing. 

## Level 3: Basic authentication

 You can upgrade your Netlify account for basic site wide authentication if necessary. It is similar to the level two encryption but is less rough around the edges, it does not use encryption, and there is no page slow down once you have authenticated. It will cost you $20 a month or thereabouts.


## Make your site searchable!

::: callout
If you want to open up your site to Google and other search engines, simply remove or rename the **robots.md** file from the root of your project.  (Or change the template to reflect the robots file of your liking.)
:::

## Remove noreferrer attributes!

::: callout 
If you want your outbound links to send referrers, edit the **mdIterator** plugin settings in your .eleventy.js configuration file to change these settings for external links. Simply remove the reference to "noreferrer" as shown below:
:::


```
.eleventy.js 

  eleventyConfig.setLibrary("md", markdownIt(options)
    .use(mdIterator, 'url_new_win', 'link_open', function (tokens, idx) {
      const [attrName, href] = tokens[idx].attrs.find(attr => attr[0] === 'href')
      if (href && (!href.includes('franknoirot.co') && !href.startsWith('/') && !href.startsWith('#'))) {
        tokens[idx].attrPush([ 'target', '_blank' ])
        tokens[idx].attrPush([ 'rel', 'noopener' ]) 👈 remove noreferrer from this line!
      }
    })
```

You should leave the **noopener** in place unless you also remove the call to **target _blank**, in which case you can probably just remove this whole plugin!

## Don't forget Github

::: callout 
If privacy is a top priority, don't forget to set your Github repository to private also!
:::