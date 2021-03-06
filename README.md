# txt2tags website

Here you will find the files for the full http://txt2tags.org website.

After editing a source `.t2t` file, remember to convert it.
A single `txt2tags file.t2t` is enough, since all the conversion
options are inside the file itself.

**IMPORTANT:** Please preview the results in your browser before
committing the changes to GitHub.

After the commit, your changes will take some time to appear at
the txt2tags website. A cronjob at the web server will do a
`git pull` once a day at noon (UTC). You don't need to worry about it.

Some files seems to be missing. But they're not! They're included
directly from GitHub. See `.htaccess` for details.

## Linking GitHub files 

There's a copy of https://github.com/txt2tags/doc inside the web server root,
so just use http://txt2tags.org/doc/
as the base URL to link any document inside it. HTML documents will be
rendered and UTF-8 is the default encoding, so you won't have any
problem showing a document. For example, to link the French man page:

http://txt2tags.org/doc/French/manpage-fr.html

To show files that are not inside the `/doc` folder, use the
GitHub raw link. The raw root URL is:

https://raw.githubusercontent.com/txt2tags/txt2tags/master/

So, for example, to make a link to the Creole sample:

https://raw.githubusercontent.com/txt2tags/txt2tags/master/samples/sample.creole

There's one caveat: HTML files won't be rendered, their sources will be shown:

https://raw.githubusercontent.com/txt2tags/txt2tags/master/samples/sample.html


## Docs path 

The `doc` folder is special for the website. Its location changes in
the web server, to be contained inside the root folder.

```
GitHub structure:
    https://github.com/txt2tags/doc
    https://github.com/txt2tags/website

Web server structure:
    /index.html
    /doc/
```

So keep that in mind when writing or editing pages.

If you need to include the contents of a document inside a page,
use the `../doc/` path. If you are making a link to a document, use
the `doc/` path. Example:

```
%!include: ../doc/English/markup/markup.t2t

See the [Markup Demo](doc/English/markup/markup.html) document.
```

You must have both [txt2tags/website](https://github.com/txt2tags/website)
and [txt2tags/doc](https://github.com/txt2tags/doc) repositories
cloned in your machine, inside the same directory.


## .htaccess 

The magic of using other GitHub files in the website happens here.
Redirection of moved and deleted files too.

If you don't know what htaccess is, please DO NOT edit it.
You may break the full website doing so.

If you're comfortable with htaccess, the comments inside the file
should be enough to guide you.

## Convert full site 

If you alter files inside the `inc` folder, such as `config.t2t` or
`footer.t2t`, you will need to reconvert all the files.

```
cd ~/github/txt2tags/website/
../tools/html-update.sh -f -c
txt2tags sample-full.t2t
```

You must have both [txt2tags/website](https://github.com/txt2tags/website)
and [txt2tags/tools](https://github.com/txt2tags/tools) repositories
cloned in your machine, inside the same directory.

> Note: An error will appear when converting `index-old.t2t`.
> That's ok, this file isn't meant to be converted.

## Update docs 

The docs and their translations are read directly from GitHub. A cronjob
at the web server will keep them updated. You don't need to worry
about it.

The only exceptions, that need to be converted manually are:

- website/sample-full.t2t
- website/manpage.t2t
- website/markup.t2t

Because they add the website layout around the GitHub document.

## Special updates 

### Update executable version (http://txt2tags.org/txt2tags.py)

It must always point to the current stable release.
Edit `.htaccess` and search for lines like these:

```
Redirect temp /txt2tags     https://raw.githubusercontent.com/txt2tags/txt2tags/2.6/txt2tags
Redirect temp /txt2tags.py  https://raw.githubusercontent.com/txt2tags/txt2tags/2.6/txt2tags
```

### Update markup.zip

```
cd txt2tags/website/
rm -f markup.zip
cd ../doc/English && zip -q -r $OLDPWD/markup.zip markup && cd -
unzip -l markup.zip
```

### Update User Guide

```
./txt2tags/doc/English/userguide/htmlgen
```

## Legacy files 

- index-old.html
- index-old.t2t
- misc/history.html
- misc/history.t2t
- misc/oldnews.html
- misc/oldnews.t2t
- misc/pt-comentarios.html
- misc/pt-comentarios.t2t
- misc/pt-enquete.html
- misc/pt-enquete.t2t
- misc/top-secret.html

These are old files that are kept for history purposes.

DO NOT convert `index-old.t2t`. Leave it untouched.

