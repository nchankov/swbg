# SWBG - Static Weblog Generator

This is a static weblog generator which would create a simple static blog site from markdown files. The project consists 
of few bash scripts which would generate static html files from markdown files. It is a simple and lightweight solution
for creating a blog without the need of a database or a complex CMS.

## How to install

Clone that repository in your local machine:

```bash
git clone git@github.com:nchankov/swbg.git
```

The swbg folder is independent from the content of the blog, so you can move it anywhere you want.

## How to use

In the swbg folder there is an `example-project` folder. It could be used as a template for your own blog project.
In the folder there are the folloing folder structure:

### ./src
this is the place where markdown files should be placed. In the src folder there is a sub folder for `assets/img` where 
you could place images which would be used in the posts. The images could be used as in the cover image of the post or 
inside the post content.

### ./templates
this is the place for the html templates which would be used for the posts list and post details page 
would be found. Read moe about the templates structure below.

### ./dist
this is the output folder where the generated static html files would be placed.

### ./draft
You could add one or many other folders, like `draft`, `private` etc. These folders would be ignored during the 
generation of the static html files, but could be used to organize your scheduled posts or drafts.

## Structure of the html templates

There are 3 main files in the `templates` folder:

### index.html
This is the template for the posts list page. 

Placeholders in that file:

{{title}}           - This would be replaced with the `Articles - Page {n}` where {n} is the page number
{{body}}            - this is where the list of posts would be placed. You can't do much with it apart from placing it 
                      in the correct place in the page template
{{first_excerpt}}   - this would be replaced with the excerpt of the first post in the list, useful for meta description
{{page}}            - this would be replaced with the current page number it would be useful to indicate on what page 
                      the user is on if there is a pagination

### article.html
This is the section of the template which is looped for each post in the posts list page. 

Placeholders in that file:
{{link}}     - this would be replaced with the link to the post details page
{{featured}} - this would be replaced with the cover image of the post
{{title}}    - this would be replaced with the title of the post
{{excerpt}}  - this would be replaced with the excerpt of the post

### page.html
This is the template for the post details page.

Placeholders in that file:

{{featured}} - this would be replaced with the cover image of the post
{{title}}    - this would be replaced with the title of the post
{{body}}     - this is where the content of the post would be placed

## Common placeholders
There are some common placeholders which could be used in any of the templates:

{{year}}     - this would be replaced with the current year during the generation of the static files
{{date}}     - this would be replaced with the current date (YYYY-MM-DD) during the generation of the static files

## Markdown file structure
Each markdown file should have the following structure:
```
---
title: Title of the post
description: Short description of the post
featured: path/to/featured/image.jpg
---
# Title of the post
Regular markdown content goes here...
```
The header (the first few lines wrapped with ---)would be used to generate the post details in the post list

## How to generate the html files

To generate the static html files run the following command from the `swbg` folder:

```bash
./generate.sh --project /path/to/your/project
```

This would generate the static html files in the `dist` folder of your project. along with a sitemap.xml file.

## How to style the blog
You could add your own CSS file in the `src/assets/css` folder and link it in the `index.html` and `page.html` templates.
Alternatively this could use the parent's site CSS if the blog is part of a bigger site.

## .env file
In the content folder you could ass a .env file (you can find an example in the `example-project` folder). There you can
change the default positions of the template folders, how many articles per page in the posts list, location to create 
the static html files.

## Hint
The dist directory could be a link to another location. For example:

```bash
/var/www/html - this is the main website
/var/www/html/blog - this is the blog
/home/user/blog - this is the blog source folder containing src, templates etc.
```

So instead of having dist folder into /home/user/blog/dist make a symbolic link from /var/www/html/blog to 
/home/user/blog/dist e.g.

```bash
rm -Rf /home/user/blog/dist
ln -s /var/www/html/blog /home/user/blog/dist
```

This way the files would go directly into the correct directory.