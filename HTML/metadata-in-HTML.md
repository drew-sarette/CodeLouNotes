# Metadata in HTML
The head of an HTML document is the part that the browser does not render. It contains meta-data, which give the browser important cues on how to render the rest of the page successfully. It also contains info used by search engines to describe the contents of the page.

## Title 
contains the title for the page, which is displayed in the browser tab. Not to be confused with ```<h1>``` which is the title of the document.

## Setting the Character Encoding
Use ```<meta charset="utf-8"/>``` to set the character encoding. UTF-8 is the standard because it includes all characters from all human languages. If you use a smaller charset, say ISO-8859-1, anything outside of that charset will be rendered as unlegible alienese, also known as "mojibake"

## Other meta elements
Many meta elements contain name and content attributes. For example:
```
<meta name="author" content="Drew Sarette">
<meta name="description" content="This is what my site does: X, Y, Z..."/> 
```

The description has the potential to help your site appear higher in search engine rankings (SEO)

The meta tag should also specify an author: 
```
<meta name="author" content="Drew Sarette">
```

Companies such as facebook and twitter have proprietary metadata that can be used to display a logo, title, and description when your site is linked to on their's:

```
<meta
  property="og:image" content="https://developer.mozilla.org/static/img/opengraph-logo.png" /> 
<meta 
  property="og:description"
  content="The Mozilla Developer Network (MDN) provides
  information about Open Web technologies including HTML, CSS, and APIs for both Web sites
  and HTML Apps." />
<meta 
  property="og:title" content="Mozilla Developer Network" />
```
OG stands for Open Graph Data, which facebook invented to provide more info to its users.

## The Favicon
Short for "favorites icon", it is a 16px square icon displayed in the browser tab and also next to bookmarked pages int he bookmarks panel.

It is wise to always add a custom favicon, as default favicons can give hackers clues about how the site was built.

To add a favicon:
1. save it in the same directory as the site's index page, in .ico format (.gif and .png are sometimes supported)
2. link to it in the head: 
```<link rel="icon" href="favicon.ico" type="image/x-icon" />```

Other links to icons can be used for specific devices. For example, this provides a high quality icon for iphones to use when the page is saved on the home screen: 

```<!-- third-generation iPad with high-resolution Retina display: -->
<link
  rel="apple-touch-icon-precomposed"
  sizes="144x144"
  href="https://developer.mozilla.org/static/img/favicon144.png" />
```
## Scripts and stylesheets
CSS should be separated into its own file andlinked to in the head: 
```<link rel="stylesheet" href="styles.css" />```
 
There are several ways to load scripts into your HTML, but the best way is to include a script tagin the head, with a src attribute containing the path to the script, and defer, which instructs the browser to load the file after the HTML is loaded.

```<script src="my-js-file.js" defer></script>```

## Setting the language
For accessibility and better SEO, set the lang attribute for the page in the opening html tag:
```
<html lang="en-US">
  …
</html>
```
You can also set the language attribute for subsections by adding a lang attribute to child elements.

For information on links: [ISO 639-1](https://en.wikipedia.org/wiki/ISO_639-1)
