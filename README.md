HackSoc.org rewrite
===

This build system is based on [Node.js][nodejs] and [Handlebars]. It replaces the [previous system][Hakyll], which used Haskell and Hakyll.

## Writing content

### Index/home page
As this includes the most recent news articles, editing the homepage is done through `index.handlebars`. The 5 most recent news articles are rendered via `newslist.handlebars`, then `index.handlebars` itself is rendered, and finally passed to `wrapper.handlebars`. Note when adding events that every other `div.infobox` must also have the `alternate` attribute.

### 'Regular' pages
These can be found in `regular/`, and consist of a YAML header and a HTML body, which is inserted into the template `wrapper.handlebars`.

#### YAML fields
 - **title**: put into the `<title>` element of the page.

### News articles
Written in [Markdown], with a YAML header:
 - **title**: the title of the article, put into the `<title>` and `<h1>` elements and shown in the list of news articles.

The first paragraph of the article is shown as an excerpt in the news article list, Markdown requires a blank line (not just a single newline) to indicate a new paragraph.
### Minutes
For the moment, minutes are in PDF form and are put into `minutes/`. These are copied into the web directory, along with an index page which lists all the minutes in the directory. The filename format is `YYYY-MM-DD-meeting name.pdf`. Regular committee meetings are simply `YYYY-MM-DD-Minutes n.pdf`. The minutes page sorts these in ascending date order based on the filename, so omitting the date will cause this to fail.

### Templates
Most of the site is generated through the `wrapper.handlebars` template. This takes the content of the page, the title, plus some global values found in `templates/context.yaml`:

 - `servers`: controls the list of servers on the website banner
    - `name`: name of this server (capitalised, hostname only)
    - `href`: link to this server's README (typically just `http://<hostname>.hacksoc.org/`).
 - `nav`: links for navbar
    - `text` and `href`: fairly self-explanatory


### Server READMEs
Written in [Markdown]. Like regular pages, has a YAML header:
 - `hostname`: lowercase hostname of the server
 - `fqdn`: full domain of the server, typically `<hostname>.hacksoc.org`
 - `name`: purpose/subtitle of the server (eg "shell server")

Don't worry about a H1/title, it's generated by the template. All headings in the document should be H2 or below (`##`).

## Installation
### 0. Prerequisites:
You'll need [Node.js][nodejs] (with npm) to install and run this.
<!-- maybe add a quick link to install scripts? -->
### 1. Clone this repo:
```
$ git clone git@github.com:HackSoc/HackSoc.org
```
### 2. Install dependencies
```
$ cd hacksoc.org/
$ npm i
```
### 3. Run
```
$ node .
```
This builds the site to the output folder `html/`, you need to run this command every time the content updates in order to keep the web version up-to-date.

## Adding features

[nodejs]: https://nodejs.org/en/
[Handlebars]: https://handlebarsjs.com/
[Markdown]: https://daringfireball.net/projects/markdown/syntax
[Hakyll]: https://github.com/HackSoc/hacksoc.org/tree/hakyll-last