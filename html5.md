# Intro

# SEO

## What HTML5 Means For SEO:

- Standard HTML tags (e.g.title, h1, etc.) form the basis of on-page SEO. Search engines use these tags to better understand what a page is about. Optimizing these factors is a basic SEO practice to improve rankings in the search results. HTML5 has provided us with a couple of new semantic elements that we might want to consider when optimizing our page.

## What’s a Semantic Element?

- Semantic Elements refer to HTML elements that have a specific meaning.
- For example `<h1>` is a semantic element. It tells google bots that the content within the tag is the most significant header contained in the HTML document. `<div>` on the other hand, is a non-semantic element as it only indicates a division in the HTML document and provide no information on what goes before, after or within the tag.

## New Semantic Tags in HTML5

- `<main`>: The `<main>` tag encloses the dominant content of the blog including all article content and other related sections that extend the central theme of the page, such as the `<article>` tag and supporting `<section>` tags.
- `<article>`: The `<article>` tag makes it easy to mark new blog posts or article entries in an online publication. Search engines can put more weight on any content wrapped with this tag. It also helps to clean up the HTML code by reducing the use of `<div>` tags.
- `<section>`: Blog posts are typically broken into different sections to make it easier for users to find what they are looking for. The `<section>` tag can be used to specify these subsections of your content, each with their own separate HTML heading. The `section` tag is similar to the `div` tag, but it is more meaningful since it wraps logical groups of related content (e.g. a chapter of an article). The section tag can be also used to wrap the article itself, but we have the article tag for that purpose.
- `<header>`: The `<header>` tag is similar to the `<h1>` tag in that it can be used to specify the header of a page. But it can also be used to indicate the header section of a page and can even contain navigation links and other relevant text.
- `<footer>`: While not as useful as the `<header>` tag, the `<footer>` tag still offers SEO benefits as it can be used to specify content in the footer section of a website such as company information and other useful links. Each page can even have its own footer section.
- `<nav>`: Navigation is undoubtedly one of the most important aspects of a site. The `<nav>` tag can be used to specify links on a page such in the main site navigation or for pagination.
- `<video>`: The `<video>` tag is easily one of the most useful tags as it allows for cross-browser compatibility to display videos without having to use Flash. HTML5 also makes it possible to include additional information about the video such as captions and subtitles.
- `<aside>`: An `<aside>` tag can be like a section tag, but one that focuses on secondary content such as sidebar, or a post-article call to action might be a good place to use `<aside>` tags. An additional content, unimportant for understanding an article, but related to the article, can be inserted into the aside section. For instance, it could be information about how many people read the article, who is the author of the article, and so on.
- `<mark>` – Used to help browsers identify important content or something that is highlighted
- `<figrure>` - The figure tag is used to mark up photos, code blocks, diagrams, charts, illustrations, and other graphic content. Generally, this tag encloses content that can be moved away into an appendix
- `<figcaption>` – The figcaption tag represents a caption or legend for a figure. It's optional and can be omitted. Only one figcaption tag can be nested into the figure tag. Even if a figure contains multiple images, there can be only one figcaption for all of them.
- `<time>` – Helps defining time
- `<hgroup>` – Aids in identifying a group of header tags
- Examples:
  ```html
  <html>
    <head>
      <title>Example</title>
    </head>
    <body>
      <header>
        Here goes logo, navigation, etc.
        <nav>
          <a href="index.html">Home</a>
          <a href="services.html">Services</a>
          <a href="contact.html">Contact</a>
          <a href="about.html">About Us</a>
        </nav>
      </header>
      <main>
        <article>
          <h1>JavaScript Basics</h1>
          <p>JavaScript is a rich and expressive language...</p>
          <section>
            <h2>Syntax Basics</h2>
            <p>Understanding statements, variable naming, whitespace...</p>
          </section>
          <section>
            <h2>Operators</h2>
            <p>Operators allow you to manipulate values...</p>
          </section>
          <section>
            <h2>Conditional Code</h2>
            <p>
              Sometimes you only want to run a block of code under certain
              conditions...
            </p>
          </section>
          <aside>
            <p>Viewed by 1503 people</p>
            <p>Author: John Smith</p>
            <figure>
              <img src="John Doe.png" alt="John Doe" />
              <img src="Maggie Smith.png" alt="Maggie Smith" />
              <img src="Tom Hardy.png" alt="Tom Hardy" />
              <figcaption>People who liked the article</figcaption>
            </figure>
          </aside>
        </article>
      </main>
      <footer>Footer information, links, etc.</footer>
    </body>
  </html>
  ```
- `Microdata`
  Microdata provides additional information about the content of a web page and helps search engines and screen readers operate on the site. Microdata can be added as attributes to any HTML tag. For instance, let's add some data about the author of the article in our example. The aside section of the article will have the following code:

```html
<aside>
  <p>Viewed by 1503 people</p>
  <p>
    Author: John Smith, Senior Software Developer at Google, Mountain View,
    California
  </p>
</aside>
HTML With microdata included, the HTML code of the aside section will be:
```

```html
<aside>
  <p>Viewed by 1503 people</p>
  <p itemscope itemtype="http://schema.org/Person">
    Author:
    <span itemprop="name">John Smith</span>,
    <span itemprop="jobTitle">Senior Software Developer</span>
    at
    <span
      itemprop="worksFor"
      itemscope
      itemtype="https://schema.org/Corporation"
    >
      <span itemtype="name">Google</span>,
    </span>
    <span
      itemprop="address"
      itemscope
      itemtype="http://schema.org/PostalAddress"
    >
      <span itemprop="addressLocality">Mountain View</span>,
      <span itemprop="addressRegion">California</span>
    </span>
  </p>
</aside>
```

- There is obviously much more data in the code above than in the previous code, but there is also much more information for machines. As you could notice, we used the following microdata attributes: `itemscope, itemtype and itemprop`. So, what do all these attributes mean?

  - `itemscope` indicates a new group of microdata. A group of microdata is called item. Items contain pairs of properties and values. The type of an item is specified by `itemtype`. This is actually a URL to a web page that contains information about the item. On that page, we can see all the properties the item could have.

  - We usually use only several properties to describe an item and we define these using the `itemprop` attribute. A value of a property can be a new item (like address in our example).

  - We mentioned before in this tutorial that a banner can be described with microdata. So, the HTML code for that should look like this:

```html
<div itemscope itemtype="https://schema.org/WPAdBlock">
  <a href="site.com" itemprop="url"
    ><img src="banner.gif" alt="banner" itemprop="image"
  /></a>
</div>
```

- There is a very useful tool for generating microdata called the Microdata generator. It can save time and teach you how to use microdata properly for various items.

## Reference
- http://webcode.tools/microdata-generator
- https://www.pluralsight.com/guides/semantic-html
