---
title: Untitled static site generator
x-toc-enable: true
...

Introduction
============

You can download the latest version of Untitled here:\
<https://untitled.vimuser.org/>

Refer to the above URL for documentation aswell. This README is merely an
introductory text.

If all you want to do is write code, and have a website documenting your
software, then `untitled` is for you! This software originally had another name
but it was decided that `untitled` is a perfect name for this very generic,
lightweight and very, very simple software.

It is named *untitled static site generator* because of a lack of desire to
come up with a better name. It is one in a million. There are many other
static site generators. Untitled is not the first, and it will not be the last!

Introduction
============

Untitled is a static site generator. It is written in Bash, and it runs
pandoc to generate HTML pages. It is a *multi-site* static site generator.
It is intended for simple websites, particularly Free Software projects that
want a full website but don't want to bother with more complicated web based
publishing systems, or who don't want to mess around with HTML.

You write pages in Markdown, as *.*md files. The variant of markdown is the
Pandoc variant, which you can read about here:\
<https://pandoc.org/MANUAL.html>

Pandoc can convert between *many* formats, but Untitled only supports converting
from Markdown into HTML. It is written precisely and exclusively with the goal
of making it easier for Free Software projects to create their own websites.
This is to fight against the trend of crappy github-powered websites that
plague the internet. It is highly desirable to see a return to the days where
software projects have websites!

History
-------

This software is very new, so expect some rough edges, and funky looking
websites! Here are some websites that already are built using `untitled`:

* <https://untitled.vimuser.org/> (official homepage of the untitled static
  site generator!)
* <https://libreboot.org/>
* <https://vimuser.org/>
* <https://blog.vimuser.org/>

Actually, it's not new at all. This static site generator was originally
written for the [Libreboot project website](https://libreboot.org/) in 2017,
but it was *much* simpler and even more broken than the version you're now
reading about. That (very simple) generator was forked many times, across
different websites, with different features added.

The *untitled* static site generator was created to combine the features of
all the forks. Untitled static site generator was created by Leah Rowe, who
also leads the Libreboot project. Untitled is heavily based on the original
static site generator written by Alyssa Rosenzweig for the Libreboot website.

Untitled is *Free Software*. See the COPYING file included with
the *untitled static site generator*. Learn more about Free Software:\
<https://www.gnu.org/philosophy/free-sw.html> (basically, it means that *you*
have control over your own copy, to do whatever you want with, and you could
even fork it to make your own version if you wished)

Requirements
============

Untitled is designed to be stupidly simple. You need:

* GNU+Linux operating system (BSD will probably also work)
* Pandoc
* GNU BASH
* SSH access to the web server you intend to use it on for site hosting, OR:
* sysadmin of the web server put untitled's `build` script on a crontab, or
  something similar, to automatically run it every now and then. and then you
  simply upload your markdown files. E.g. shared hosting provider running
  `untitled`.
* Web server (nginx recommended)
* RECOMMENDED: chroot environment. Run the scripts (for generating web pages)
  in a chrooted environment. This is for security purposes.
* RECOMMENDED: disable symlinks in your web server, for any website built using
  this software.
* Willingness to use incredibly fragile, unstable code to power your website.
  This static site generator is very experimental. It is used by its lead
  developer, Leah Rowe, to generate
  the [Libreboot website](https://libreboot.org), but it is HIGHLY recommended
  that you read the code for Untitled, and familiarize yourself with it fully,
  before you decide to use it. It's not in a state right now where you can just
  use it. In all likelihood, it's going to annoy you in some way by not doing
  something you want, so you'll have to tweak it. Patches welcome!

NOTE FOR HOSTING PROVIDERS: DO NOT USE THIS SOFTWARE YET! It's very unstable,
and highly experimental. The authors of this software are not responsible if
your website gets nuked.

It is assumed that you have a BASH shell on the server you're using to host
sites on. E.g. physical access, SSH, serial console, whatever.

There are actually plenty of other programs already that can let you host a
website with Markdown files. Untitled is yet another static site generator.
It is Leah's pet project, but one day it might grow into something great.

Security warnings
=================

Disable symlinks in your web server.

Also, the logic is barely audited. It is very hastily written, to meet a goal.
This software was only very recently released (17 May 2021 was the day this
software became available on the internet); as such, it is to be considered
alpha (even pre-alpha) quality.

TO BO CLEAR: if you value your data, do not use this software in production.
In it's current state, this software is *poorly written*.

ONE MORE TIME:

DO NOT USE this software in production, unless you're either insane or you know
how to avoid common security pitfalls, because this software is *not* secure.
At the very least, you should be running this in a chrooted environment.
If you're Leah Rowe, everything in this paragraph is true.

NOTE: disabling symlinks in your web server only affects what the public can
access, but `untitled` currently doesn't check for symlinks when *building*
a Markdown file into HTML locally. This means that you SHOULD NOT USE IT
unless you can control accesses to the repository where your markdown files
are hosted.

So for instance, if you're a software project with lots of people having push
access to a Git repository hosting your documentation site, don't have untitled
automatically run, because a real bastard could potentially pwn you.

This notice will be removed when this bug is fixed.

Basically, don't run it automatically. If you're the only one with push access
to your repositories and/or websites, and can absolutely control everything,
it's safe, but please DO be vigilant against this.

Anyone with basic knowledge of security (or the concept of opsec) knows this,
so there's no point in hiding it.

There *is* a workaround: run `untitled` in a chroot environment, on your server.
A properly configured chroot environment should be OK.

Getting started
===============

Simply make a directory named `www/` in the root of your untitled software
directory.

In `www/`, make a directory *per website*. For each website,
set `www/sitename/site/` as the document root in your web server.
Untitled expects this `site` directory to exist.

Example website
---------------

Check the `www-example` directory, for an example website. Also look at the
logic in the file named `build`, in the main directory of the untitled static
site generator.

You can actually copy this directory and rename the copy to `www` if you wish.
When you've done that, you can compile it into a website.

You can probably figure out how to get your own site working, but read on if
you need further guidance.

How to use
==========

Untitled is written on a GNU+Linux system. It is expected that you will
interact with it on a shell, specifically GNU BASH. Make sure that you have
the *latest* version of Pandoc installed!

See:

* <https://www.gnu.org/software/bash/>
* <https://pandoc.org/>

Generate a website
------------------

To interact with `untitled`, your current working directory should be the main
directory *of untitled*, *not your website*. In that directory, the file named
`build` and the file named `clean` will exist.

For a given directory name under `www/`, do this:

    ./build www/directoryname

You can also do:

    ./build directoryname

For example, if your website was hosted at www/foobar:

    ./build foobar

This will only work if your website is set up correctly. Look at the example
website in `www-example/` and read the sections below.

To build *all* available websites under `www/`, just run it without an argument:

    ./build

You can specify *multiple* websites. For example:

    ./build blogsite catblogsite

In this example, the following sites would be built:

* `www/blogsite`
* `www/catblogsite`

Cleaning up
-----------

If you want to un-make your site, such that the HTML files are purged, do this:

    ./clean

This will clean *all* sites. If you only want to clean a specific site, do
this:

    ./clean sitename

(sitename would be located at `www/sitename/`, in this example)

NOTE: an HTML file is only deleted if a corresponding Markdown file exists.
This means that if you permanently delete a markdown file from your site, you
should ensure that the HTML file is also delete dif you don't want that file
to be available anymore.

Markdown files
==============

Write your markdown files, with file extensions ending in *.*md and the build
script will automatically see them. It will convert them into HTML, stripping
off the *.*md file extension and replacing it with *.*html

Place these markdown files anywhere under `www/sitename/site/` where `sitename`
is whatever you named your website, per directory hierarchy rules of Untitled.

Again, the `www-example` directory can be extremely useful if you want to play
around first, before you make a real website with Untitled.

Global files per site
======================

These files affect the site globally, for each website under `www/`

www/sitename/site.cfg (REQUIRED)
--------------------------------

sitename can be anything.

site.cfg is the main configuration file for your website.

Example entries (for libreboot.org):

    TITLE="-T Libreboot"
    CSS="--css /global.css"
    DOMAIN="https://libreboot.org/"
    BLOGDIR="news/"

### BLOGDIR

This is the directory for your main news section, if you have a news section.
You do not need to declare this.

The news section is only valid if it has the right files, in the directory
specified here. You can actually have as many news/blog sections as you like,
but this setting specifies the "main" one. For example, if you're a software
project you might have a news section, and a release section, and they might
both be news pages. News pages have RSS feeds and indexes automatically
generated by `untitled`.

If your website is primarily a blog, you might leave this string empty. That
way, your *home page* is the news index. In that scenario, you would not place
an index file in the root of your website. Let `untitled` generate it for you!

### DOMAIN

This is the URL for the home page of your website.

### CSS

Specifies the .css file, or files, to be used. See above example. Just add
entries saying `--css /path/to/css/file` for each CSS file. The `/` is the root
of your website, when viewed publicly. Basically, / would be the home page,
and everything after that is relative. In other words, it is the URI of your
CSS file.

### TITLE

Use the format above. Don't use spaces or special characters. Just keep it
simply. E.g. `-T Gardening`

This would usually be the name of your website, company, project or whatever
else.

www/sitename/site/template.include (REQUIRED)
---------------------------

Put a pandoc template here, in this file.

There is an HTML5 template in `www-example/` which you can adapt for your site.
TODO: make an xhtml template. Patches welcome!

It is recommended that you put your common site navigation section in this
file (formatted in HTML).

www/sitename/site/nav.include (optional)
----------------------

Put this in the root of `www/sitename/site/`. You can actually put whatever
you want in here, but it can be used for a navigation menu. You could also use
it to put a side-wide notice, on your website.

Write this file in Markdown. You could also put a common navigation section
in the template, and use `nav` files for site-wide announcements, or for
announcements on specific pages. How you use Untitled is entirely up to you!

www/sitename/site/global.css (optional)
----------------------------

The filename can actually be anything, for your CSS. In fact, it's entirely
optional. You can leave the CSS string empty in `site.cfg` and just have a
site without CSS.

The name `global.css` is merely what the example website (in `www-example/`)
uses, but you don't have to use this file name yourself.

This file is for styling your pages (HTML ones, after building your Markdown
files).

w3schools has a nice set of tutorials for learning CSS:

<https://www.w3schools.com/css/>

www/sitename/site/sitemap.html
-----------------------------

The file named sitemap*.*md will be automatically generated, which is then
assembled into `sitemap.html`. This file will sit on the root directory of
your website.

Do not manually create these files. They are automatically generated by
Untitled. They simply index your entire website.

NOTE: It only looks at pages where a Markdown file exists. It ignores pages
where an HTML page exists but a Markdown page doesn't.

www/sitename/site/sitemap.include
---------------------------------

This file MUST be included if you want a sitemap.

Simply put a title and some text in here. Untitled and Pandoc will do the rest!

www/sitename/site/footer.include
--------------------------------

If present, this will add a common footer to every page on your website. Write
it in Markdown.

Rules for *.*md files in www/sitename/site/
===========================================

This applies to any *.*md file under `www/sitename/site/` where `sitename` is
whatever you named your website, per directory hiearchy rules.

The file named file*.*md will be converted into HTML and copied (in HTML format)
to `file.html`.

When you link to other pages, use absolute links or relative links, but don't
link to the `.html` pages. Link directly to the *.*md files. Untitled static
site generator will use Sed to replace these with .html when generating the
HTML pages (it only skips replacing *external* links,
e.g. `https://example.com/cats.md`

TOC (Table of Contents)
-----------------------

See pages in `www-example/` or example websites linked above (such as the
Libreboot project website). Look in the markdown files for those sites, on
pages that specify `x-toc-enable: true`. This is a special directive for the
Pandoc variant of Markdown. Some other Markdown parsers/generators will also
generate a table of contents.

In the untitled static site generator, when a TOC is enabled, the depth is 4.
This means that, in HTML, the h1, h2, h3 and h4 tags will show up on the TOC.
The TOC is generated *based on* how you use headers in Markdown, and how they
ultimately end up when converted into HTML.

file.nav
-------------

If present, the page from file*.*md will have its own navigation menu, which
will override the default nav.include file.

This can be anything. Write it in Markdown. For example, you could use this to
put announcements on a page.

file.css
--------

Where you have file*.*md, you can also include `file.css`, and this CSS file
will be applied specifically to that page.

This does not replace any global CSS files that you specified in `site.cfg`. It
is applied *after* that one. One possible use-case for this is if you have an
otherwise decent CSS file for your site, but you need to override certain
rules on a specific page.

file.template
-------------

Where you have your Markdown file, strip off the `md`, you create a new file
with the same name but with `.template` file extension. This will override the
default, global template, for that page only.

file.footer
-----------

If present, this replaces the global footer for the specific page.

News sections
-------------

This section defines what files should be placed in directories that are to
be news sections. For instance, you might have a directory on your website
named `news/`, and you would place these files in that directory.

An index page will be automatically generated, so don't bother making one
yourself. Simply write your news pages. Read the notes below for how to set up
news sections on your website.

An RSS feed will also be generated, for every news section.

*You can have as many news sections as you would like!*

### Rules for news pages

A table of contents is always enabled, on news pages (but not the news index),
unless you want it to be so. Technically, news indexes have a TOC but the page
isn't formatted such that a TOC will appear when Pandoc does its thing.

Start your news page like so, in the Markdown
file e.g. www/catblog/site/news/spots-birthday*.*md

    % Page title
    % Author name
    % Date
    
    Page text goes here

### MANIFEST

Place this file in the root of the directory where you want there to be a
news section.

The order of the file names dictate what order the links will appear in, on
the news index that is automatically generated (see below).

### news-list*.*md.include

This will have a page title, and introductory text. When the index page is
generated (see below), the resulting index will include the contents of this
file, and then links to each page per the contents of `MANIFEST`.

### index*.*md and index.html

Do not place these files in directories containing a MANIFEST file. These will
be generated automatically, with an index linking to news articles.

### news.cfg

In this file, write the following lines:

    BLOGTITLE="The daily grind"
    BLOGDESCRIPTION="Hot takes, juicy gossip and everything inbetween!"

You can change these strings to whatever you want. Keep it simple! For
example:

    BLOGTITLE="Bianca's worldly musings"
    BLOGDESCRIPTION="Come see what I'm thinking about! I have many thoughts"

For news about your software project, you might say:

    BLOGTITLE="Project announcements"
    BLOGDESCRIPTION="News about ongoing development will be documented here"

### RSS files

Files ending in `.rss` are automatically generated, if you have news sections.

Translated pages
================

Untitled doesn't really support multi-language sites very well, and it assumes
that you speak English. It assumes that you will write websites in English.
It's on the TODO to change this.

However! Rudimentary logic exists in the build script, for having translated
pages.

If you have a file named file*.*md, it's assumed that this page will be in
English. If you want a Russian page, you would make a file named file.ru*.*md

If you made an override file such as file.nav, file.css. file.template or
file.footer, it will also apply on file.ru*.*md

The language is also inserted into the page as e.g. `lang=ar` in the main HTML
tag. Also: if Hebrew (.he) or Arabic (.ar), untitled knows already to set the
text order right-to-left instead of left-to-right.

If you wanted to have a page that is primarily in English, but you wanted to
have translated pages, you could make them. Fun fact: you can make a `file.nav`
and put an index there linking to all the translated pages!

As you can see, handling multi-language sites *is* possible even now, but it is
assumed that the *default* language is English! What if the site was primarily
for Chinese users, but that site also wanted an English version? Well, this
level of sophistication is not yet supported by Untitled, but it is desirable.
If you wish to implement it, please submit a patch! Otherwise, it will be
implemented at a later date. I'm (Leah Rowe here, breaking the fourth wall)
planning to have translations for pages on the Libreboot website at some point
in the future, so I will be implementing this functionality myself regardless,
if nobody else wants to do it.

Binary files e.g. videos
========================

Untitled static site generator only cares about the files specified on this
page. It ignores all other files.

For things like images, videos and other binary files, it is recommended that
you create a specific directory or subdomain for them, and have only markdown
files on your Untitled website.

However, it's up to you how you run your infrastructure.

It is recommended that you use a Git repository to host your website. Then you
can easily keep track of changes to your site. You would use a static version
of Untitled on your server, and just build new changes to your site whenever
you push them. This is actually *why* the `site/` directory is enforced under
the `www/sitename/` directory for each site, so as to encourage good practise
(because by doing it this way, the `.git` directory will not be visible on your
public web server. You do *not* want that directory to be visible!)
