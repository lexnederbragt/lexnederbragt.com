---
layout: post
title: "Announcing canvasCourseCli"
subtitle:
tags: [canvas, teaching]
---

I wrote a small command line tool (in Python) for retrieving,
adding and updating content, pages
and files exposed to students and teachers,
for a Canvas course.

## Motivation
At the University of Oslo, we started using Canvas a few years back.
Writing content for the pages of a course is normally
done through a web-interface.
However, I am very fond of writing content for the web in [Markdown](https://en.wikipedia.org/wiki/Markdown).
However, there is no option to write in Markdown directly
in the Canvas web interface.  
I also like to keep my textfiles under version control.
So, I needed a way to write course pages in Markdown, convert them to html
and upload them to my Canvas course, ideally through the command line -
another tool I am very fond of.
Since I could not find such a tool, so I decided to write my own.
After all,
Canvas is [an open source project](https://github.com/instructure/canvas-lms/wiki)
and has an [API](https://canvas.instructure.com/doc/api/index.html)!

## canvasCourseCli

Thus was born `canvasCourseCli`. It uses the Canvas API
through the Python package [canvasapi](https://github.com/ucfopen/canvasapi).
Commands start with `canvasCourseCli` followed by one of the subcommands:

```
list_files    -u URL                        List all files for a course on Canvas.
list_pages    -u URL                        List all pages for a course on Canvas.
tree          -u URL                        List all folders for a course on Canvas.
dump          -u URL                        Download all files and pages for a course on Canvas.
view_page     -u URL                        View the content of a page on Canvas.
add_page      -u URL -t TITLE -f HTML_FILE  Add a new page to Canvas.
create_folder -u URL                        Create a new folder on Canvas.
add_file      -u URL -f FILE_TO_SEND        Add a file to a folder on Canvas.
update_page   -u URL -f HTML_FILE           Update the content of a page on Canvas.
add_to_module -u URL -m MODULE_NAME         Add a page on Canvas to a module.
```

For example, if you want to replace the content of an existing page with content of a file (in html format) on your computer, for an imaginary course that 'lives' at https://instance.instructure.com/courses/9999, you could run this command:

```
canvasCourseCli update_page -u https://instance.instructure.com/courses/9999/pages/name-of-page -f file.html
```

I hope to develop more subcommands in the future.

## How I use it

* I write course pages in Markdown
* convert them to html using [pandoc](https://pandoc.org)
* upload or update them to Canvas using `canvasCourseCli`
* I use a Makefile and [Gnu Make](https://www.gnu.org/software/make/)
  to automate this process
* I also automate uploading some of the files that I add to Canvas on a weekly basis
  through that Makefile

All pages for the latest edition of my course
'BIOS1100 - Introduction to Computational Modelling in the Biosciences'
are written in Markdown and updated on Canvas through `canvasCourseCli`,
and many of the course's files are added through it too.
Feel free to view the results at
[the Canvas page for this course](https://uio.instructure.com/courses/20058).

## What about the Canvas Data CLI Tool `canvasDataCli`?
The [Canvas Data CLI Tool](https://community.canvaslms.com/docs/DOC-6600-how-to-use-the-canvas-data-cli-tool#jive_content_id_Overview) is used to extract course data from the database. `canvasCourseCli` is meant to work with course pages and files.

## How to install it

For now, `canvasCourseCli` is available through a GitHub repo
at [https://github.com/lexnederbragt/canvasCourseCli](https://github.com/lexnederbragt/canvasCourseCli).
Clone that repo, or
[download the code](https://github.com/lexnederbragt/canvasCourseCli/releases),
and make it available on your system.
I hope to make it into a 'proper' Python package,
installable through (for example) `pip`, as soon as I find time
to figure out how to do that.

Further documentation can be found in the [README file](https://github.com/lexnederbragt/canvasCourseCli/blob/master/README.md#canvascoursecli) of the repository.

### A word of warning
I have not been able to test `canvasCourseCli` on any other Canvas (instructure) instance than the one provided by my university. I would appreciate feedback (through the [issue](https://github.com/lexnederbragt/canvasCourseCli/issues) functionality of the Github repository) on *both* successful and failed attempts at using the tool for your course.

## What's next

I hope to add functionality and improve the code in the near future. There is a
[ToDo list](https://github.com/lexnederbragt/canvasCourseCli/blob/master/TODO.md)
that has my thoughts and wishes for further development. I welcome contributions!

## A note on teaching, programming and using the command line

I used to do a lot of command line based analysis on supercomputers.
These days, I mostly teach programming to novices.
However, as much as possible I try to use my 'command line and programming skills'
for my teaching work. So

* I write course materials in Markdown
or [DocOnce](https://github.com/hplgit/doconce/wiki/manual)
(another markup language)
* have all text files under version control
* convert to different formats through the command line
* automated using `make` and Makefiles where possible
* synchronize the files to Canvas with `canvasCourseCli`

Not only does this make me more efficient,
I also find it a fun way to work (and it keeps my skills up to date)!

This is my first real piece of software that I deliberately wrote
also for others to use. Pretty scary, actually!
But I realized that if `canvasCourseCli` is useful to others,
I may even get people interested in helping me to improve the tool!

Finally, when writing this program, and setting up the repository,
I aimed to follow the recommendations we wrote in
the [Good enough practices in scientific computing](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005510) paper.
I found that to be a very useful exercise!

Enjoy `canvasCourseCli` and, as I said, [I welcome contributions](https://github.com/lexnederbragt/canvasCourseCli/blob/master/CONTRIBUTING.md)!
