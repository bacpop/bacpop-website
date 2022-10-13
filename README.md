bacpop-website
==============
A [Hugo](https://gohugo.io/) website running on www.bacpop.org

Set-up
------
Run:
```
git clone --recursive git@github.com:bacpop/bacpop-website.git
```

[Install hugo](https://gohugo.io/getting-started/installing/) (with homebrew is easiest)

Run the site locally with:
```
hugo server -D --disableFastRender
```
this should appear on http://localhost:1313/

Making changes
--------------
1. Make a new branch and check it out. (e.g. `git branch update-about && git checkout update-about`)
2. Change the code for the page.
3. Confirm with the local running copy it looks how want.
4. Commit to the branch, and push it.
5. Create a pull request. You'll get a preview on netlify to confirm your changes.
6. Ask someone else in the group to review your changes.
7. If they're happy *they* can merge the branch into `main`. This will update www.bacpop.org

New posts
------------
1. Create a new post with a command such as `hugo new posts/phylogenetics.md`.
2. Write the post (using Markdown).
3. Preview locally with `hugo server -D`.
4. When ready, commit to a new branch, and set `draft: false`.
5. Follow steps 5-7 above.

Tips
----
* Have a look at some of the existing posts to see how to add images, insert pure
html to insert videos and so on.
* Images go in `static/images` and any subfolder you wish. The basic command
for inserting one is `{{< figure src="/images/fig1.jpg" title="Figure 1" >}}`.
* It's currently best to resize and change quality of images in something like photoshop
so they aren't too large, rather than using the hugo resizing tools.
* If you want to add accounts to your about me, have a look at the examples. You
can see the available types under `themes/ananke/assets/ananke/socials/`.
* To change your header image, there are some defaults 1-13 under `static/images` you
can use, but feel free to add your own. Wide aspect ratio photos look best. No need
to relate to page content!
* Logos for software and the like go in `assets/images`. See the software page
for examples of how to insert and rescale them.
* `{{< toc >}}` adds a table of contents with the second level headings.
* Use `{{< rawhtml >}}` and `{{< /rawhtml >}}` if you want html rather than markdown
in a section (e.g. for embedding videos or plots).

Advanced
--------
* If you want to change the structure of a page (header etc) you do this in
`layouts/`. The default is to use the one in `themes/ananke/layouts`, but if you
add into the top level directory this will override it. These files use the
various hugo commands and html you see in the documentation, rather than markdown.
* If you want a snippet which runs hugo code you can write one under `layouts/shortcodes`.
See `logo.html` for an example, and the software page for how these are used.
