# Eleventy
Eleventy is a Static Site Generator (or SSG). It converts a set of templates, written in EJS, Nunjucks, Liquid, etc... into a set of static pages.  The benefits of using a ssg include:
- code is DRY
- faster page load times
- improved security
- easy to manage content using markdown

## Setup
Eleventy is available as a package from npm.
To install use ```npm install @11ty/eleventy --save-dev```

in the package.json, can enter "eleventy --serve" and "eleventy" as scripts. 

Create the config file in the root directory, and name it ```.eleventy.js``` in this file, you can specify the input and output directories like this: 
```
module.exports = function (eleventyConfig) {
    return {
        dir: {
        input: "src",
        output: "public",
        },
    };
};
```

The defaults are src and _site. This function can also be used to configure eleventy to copy additional material into the output directory, such as css or assets by adding 
```
  eleventyConfig.addPassthroughCopy("./src/style.css");
  eleventyConfig.addPassthroughCopy("./src/assets");
```

## Templating structure
In whatever input dir is configured, 11ty will search for template files and output them, each in its own subfolder containing an index.html, to the output dir. These are the actual pages on the site. The main template files will have access to the template files in the /src/_includes folder. _includes contains both layout templates and snippets of html that can be plugged into the main templates.

## Template file contents
.ejs, .njk, or .md files all have ways of being connected together to render a complete html page. These examples will use Nunjucks.

to configure vscode to recognize your templating language of choice, go to settings, search for Emmet, go to Include Languages, and enter .njk with html. Then you can use emmet in your template files. Also consider installing an extension to get syntax highlighting/formatting.

You should create a base.njk file that contains the all the boilerplate HTML used by all pages on the site, including doctype, head, body and main tags.

If each page will have its own title, you can use Nunjucks to insert it into the base.njk file every time like this: 
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="preconnect" href="https://fonts.gstatic.com">
    <link
      href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700..900&family=Roboto:ital,wght@0,400;0,700;1,300&display=swap"
      rel="stylesheet">
    <link rel="stylesheet" href="/style.css">
    <title>{{ title }}</title>
  </head>
  <body>
    {% include 'header.njk' %}
    <main>
      {{ content | safe }}
    </main>
    {% include 'footer.njk' %}
  </body>
</html>
```
The title is taken from the metadata in the front-matter of each page on the site. For example, the index.njk file might contain this at the top :
```
---
title: Your page's title
layout: "base.njk"
---
```
The layout specified in the front matter tells 11ty to plug the content into the base.njk file, while the title allows you to pass in a specific value into the base.njk html for just that specific page. 

In the base.njk file above, the content from index.njk is plugged into the main tag.  the | utilizes the "safe" filter supplied by 11ty. This is used when the content is known to be something we have created and is safe to render as HTML. Without it, the html will be rendered as string. 

the {% include "...." %} statements bring in other templates from the _includes directory. This way the header and footer can be updated in one place, and then automatically coppied to every page by 11ty when the site is built!

## Data Cascade
in 11ty, data is merged from multiple sources before each template is rendered, and this is called the cascade. 
1. computed data
2. template front-matter
3. template data files
4. directory data files
5. front-matter in layout files
6. configuration API global data
7. global data files

for example, you can add a blog.json file in a blog folder containing md files for specific blog posts. Add this json object:
```
{
    "tags": "post",
    "layout": "article.njk"
}
```
That metadata will cascade down to each blog post unless it is overwritten by template front matter or computed data.
This creates easy uniformity and consolidates metadata into one location.

## Collections
Collections are groupings of content that share a tag in 11ty. Tags may be listed in the front-matter of content like this: 
```
---
tags: ["tag1", "tag2",...]
---
```

The collections can be accessed thusly:
```
{%- for post in collections.post -%}
  {{ post.data.title }}
{%- endfor -%}
```