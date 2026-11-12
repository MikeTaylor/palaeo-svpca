# svpca.org archive

A static copy of svpca.org, the website of the Symposium of Vertebrate Palaeontology and Comparative Anatomy, as it stood when it was taken down in March 2026. It was rendered from the site's own PHP code and database and needs no PHP, database or build step to serve.

`site/` is the website. Every link inside it is relative, so it works from any static host, under any path prefix, or opened straight from disk via `site/index.html`.

## Hosting

**Any static host.** Upload the contents of `site/`. All pages and links work. Old svpca.org URLs that ended in `.php` will not resolve without one of the two configurations below.

**Apache.** Upload `site/` as the document root, or any directory below it. The included `site/.htaccess` makes old URLs work. It needs `mod_rewrite` and `AllowOverride FileInfo` (or `All`) for that directory.

**nginx.** Use `nginx.conf` as a starting point: set `server_name` and `root`, and include it in the `http` block.

With either configuration, the old URL of any page in the archive, query string included, returns that page under the same URL. For example `/pages/programme.php?venuID=00000000074` and `/years/2014_york/index.php?yr=2014` both work.

## How URLs map to files

| Old URL | File in `site/` |
| --- | --- |
| `/dir/` or `/dir/index.php` | `dir/index.html` |
| `/X.php` | `X.html` |
| `/X.php?Q` | `X@Q.html`, or `X.html` if the query string did not change the page |
| anything else (images, PDFs, CSS) | same path |

The server configurations implement the third row as "serve `X@Q.html` if it exists, otherwise `X.html`".

## What is included

Every page reachable by following links from the home page, plus every page, image and document from the old site that the Internet Archive's Wayback Machine had recorded and that was still on the server. Administration, login and submission forms (including blank booking and card-payment forms) are left out because they cannot work without the PHP application.

Also included are some files that had disappeared from the server by 2026 but were recovered from the Wayback Machine: the 2010 programme and abstract booklet, the 2013 and 2017 abstracts, the 2017 first circular and sponsor logos, the 2005 logo, the 2007 circulars in RTF, and two navigation buttons on the 2000 presentation pages.

About 30 links remain broken (`linkcheck` lists them). Their targets were removed from the server and are not in the Wayback Machine either, for example images on the 2000 presentation pages and maps in the 2013 third circular.

## Differences from the live site

- **Spam removed.** In the months before it was taken down, the site's database was altered to inject SEO spam into several conference year pages: escort, sex-shop, hearing-aid and SMS-verification advertising, Georgian airport transfers, and an article about the California Lawyers Association. Some of it was hidden from view. All of it has been removed. The result was checked against copies of the same pages in the Wayback Machine from 2023 to 2025, before the spam appeared.
- **Vandalised links restored.** A link to the Jones-Fenleigh Fund page on the 2018 Manchester page, and several images and links that the site's text editor had rewritten into broken addresses (the 2016 Liverpool sponsor logos among them), are restored to what the 2023 Wayback copies show.
- **Year logos.** Conference year pages show their own logo where one exists, as they did before a code change shortly before the site closed replaced them with the generic SVPCA logo.
- **Pages that had stopped working.** The HTML circulars (for example `years/2014_york/third.circular.php`) were failing with a server error and are shown again. The Previous Years, Jones-Fenleigh Fund and Code of Conduct links on year pages, the year logo link on programme pages, and the "View" links from the 2024 programme to its abstracts now go where they were meant to.
- **No error messages.** The live site printed PHP warnings into many pages. They are gone.
- **Character encoding.** Pages declare UTF-8, which is what browsers actually used on the live site, so accented characters display correctly on any host. Text that was already garbled in the database (for example some author names in the 2024 programme) is unchanged.
- **Footer.** The "Admin" link is removed.

- **Programmes and abstracts restored.** By 2024 the programme pages for earlier years were empty: their data was in older formats that the final code no longer displayed. They are rendered again from the database for 1982–2018, and 2013, 2016, 2017 and 2018 have programme pages for the first time. Each year whose abstracts have text in the database (2004–2017 and 2023) has an abstracts page, linked from the programme's "View" links. Some old programme entries pointed at abstract numbers that were later reused by other years. Those talks are shown as "details missing" instead of the wrong talk, and a note at the top of the programme says how many are affected. The same applies to talks the database lists without any abstract. Most talks are affected in 1996, 2003 and 2018, and about half in 2013 (whose programme in the database is an unfinished draft). 2010 and 2023 have no programme data. Their programme pages point to the year's PDF programme or booklet instead.
- **Missing year pages rebuilt.** Other pages linked to the 1998 Bournemouth, 2013 Edinburgh, 2017 Birmingham and 2021 Oxford pages, but their directories had been deleted from the server. They are rebuilt from the database, with the 2013 and 2017 third circulars, and they appear on the Previous Years page. The 2021 text is taken from the 2023 Wayback copy, because the spam injection had flattened the database copy into one paragraph.
- **Documents on year pages.** The final code no longer listed circulars on year pages. Each year page now has a menu of the circulars, abstracts and programme PDFs in its directory, its programme and abstracts pages, and its photographs.
- **Gallery.** The old photo galleries no longer worked. `pages/gallery.html` (on the main menu) shows every photograph that no other page links to, with a thumbnail linking to the full-size picture. Photographs are grouped by year and by the old gallery sections, with their original captions. Old `gallery.php`, `galleries.php` and `group.php` links lead there.
- **Links repaired.** Links to files that exist under another name or path are pointed at them, for example the 2004 group photographs, the 2007 circulars, and `.php` links inside page text. E-mail addresses hidden by Cloudflare's obfuscation in saved page text are readable again. Accented characters that were double-encoded in the database are corrected in the restored pages.
