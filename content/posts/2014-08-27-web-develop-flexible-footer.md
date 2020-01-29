---
layout: post
title: 'Web Develop - Flexible Footer'
date: 2014-08-27
comments: true
categories: [html, css]
---
## Web Develop - Flexible Footer

Sometimes we think footer must fixed in website bottom or put it in last of content.

I provide a idea may be a good way.
Content less browser view height, footer fixed in bottom.
When content too much over browser view height, footer be put last of content.

### Feature

* flexible
* only use CSS

### Usage

`min-height: calc(100% - <footer height>);`

```css
    #hd {
        height: 50px;
        background: #aaa;
        /*display: none;*/
    }
    #bd {
        text-align: center;
        min-height: calc(100% - 50px); /* important */
        background: #ccc;
    }
    #content {
        padding-bottom: 60px;
    }
    #footer {
        position: relative;
        bottom: 50px;
        text-align: center;
        height: 50px;
        background: #999;
    }
```

`50px` is footer height

```html
    <header id="hd">
        <h1>Head</h1>
    </header>
    <article id="bd">
        <section id="content">
            <button>build content</button>
            <h1>Content</h1>
            <div id="loop"></div>
        </section>
    </article>
    <footer id="footer">
        <h2>Footer</h2>
    </footer>
```

[demo](http://tedshd.lionfree.net/demo/view_UI/footer.html)

[Refer - siteInspire - Web Design Inspiration](http://www.siteinspire.com/)
