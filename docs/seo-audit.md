# SEO Audit

This audit focuses on the 2 existing pages (`index.html`, `page1.html`).
The fictitious domain name is `https://devskills.example`.

- [x] Read the problem statement,
- [x] Identify 12 SEO issues:
    - [x] Group the issues by category (*HTML*, *content*, *image*, *performance*, *URL*, *navigation*, *SEO techniques*),
    - [x] Assign a severity level to each issue:
    - [x] Describe how to fix it,
- [ ] Optimize the Web pages:
    - [ ] Fix the HTML structure,
    - [ ] Optimize the links,
    - [ ] Fix the contents,
    - [ ] Suggest URLs with "justification",
    - [ ] Create `robots.txt`,
    - [ ] Create `sitemap.xml`,
    - [ ] Add a canonical URL to each page,
- [ ] Record the before/after Lighthouse scores.


The **severity levels**:

- `HIGH`: blocks indexing or ranking,
- `MEDIUM`: clear loss of ranking or of click-through,
- `LOW`: polish, no direct ranking impact



## SEO Issues

### HTML

#### 1. No `<h1>`, and no headings (HIGH)

- *Where**: [`index.html:14`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L14), [`index.html:22`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L22), [`index.html:30`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L30),
  [`page1.html:7](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/page1.html#L7)
- *Problem*: every section title is a `<div>`.  
   A crawler has no way to
   tell what each page is about, nor how its sections rank against each
   other. This is the single most damaging On-Page defect of the two
   pages.
- *Fix*: 
    - One `<h1>` per page stating its subject, then `<h2>` for each
  section, nested without skipping a level.  
    - On `index.html`, 
        - `"Formation développeur"` becomes the `<h1>`
        - `"Java Spring Boot"` and `"Nos autres formations"` become `<h2>`.

#### 2. Missing `<meta charset="UTF-8">` (HIGH)

- *Where*: [`index.html:2`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L2), [`page1.html:2`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/page1.html#L2)
- *Problem*: the content is French and contains accented characters
  (`"différentes"`, `"d'apprendre"`). Without a declared encoding the
  browser guesses, and the text can render as mojibake. Corrupted text
  is both a user-facing bug and an indexing one.
- *Fix*: `<meta charset="UTF-8">` as the first element inside
  `<head>`.

#### 3. Missing `<!DOCTYPE html>` and `lang` attribute (MEDIUM)

- *Where*: [`index.html:1`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L1), [`page1.html:1`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/page1.html#L1)
- *Problem*: 
    - With no `DOCTYPE` the browser falls back to *quirks mode*,
      which changes the box model and breaks the rendering a crawler
      evaluates. 
    - With no `lang`, neither search engines nor screen readers
      know the content is in French.
- *Fix*: Add `<!DOCTYPE html>` on line 1, then `<html lang="fr">`.

#### 4. No semantic landmarks (MEDIUM)

- *Where*: whole `<body>` of both files
- *Problem*: the pages are built entirely from `<div>` and `<a>`. The
  navigation block is a `<div class="menu">`, so nothing distinguishes
  navigation from main content, and there is no `<main>`, `<header>` or
  `<footer>`.
- *Fix*: 
    - Wrap the menu in `<nav>`, 
    - Wrap the page content in `<main>`, 
    - Wrap each formation block in `<article>` or `<section>`,
    - Add a `<footer>`.


### Content

#### 5. Duplicate and non-descriptive `<title>` (HIGH)

- *Where*: [`index.html:3`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L3), [`page1.html:3`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/page1.html#L3)
- *Problem*: both pages are titled `Accueil`.  
    The title is the
  strongest *On-Page* ranking signal and the headline of the search result. 
  Two identical titles also read as duplicate content, and
  `page1.html` is not a home page at all. 
  It is the Java Spring Boot course.
- *Fix*: a **unique, descriptive title per page**, keyword first and brand
  last, **under about 60 characters**:
    - `index.html`: `"Formations développeur à Marseille | DevSkills
      Academy"``
    - `page1.html`: `"Formation Java Spring Boot | DevSkills Academy"``

#### 6. Missing `<meta name="description">` (MEDIUM)

- *Where*: [`index.html:2`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L2), [`page1.html:2`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/page1.html#L2)
- *Problem*: no description means *Google* extracts an arbitrary snippet
  from the page, so you lose control of what appears under the title in
  the results. It does not rank the page directly, but it drives the
  click-through rate.
- *Fix*: **one unique description** per page, **150 to 160 characters**,
  written as a sales line and containing the page's main keyword.

#### 7. Keywords (HIGH)

- *Where*: [`page1.html:7`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/page1.html#L7), [`page1.html:12-13`](https://github.com/ebouchut-laplateforme/seo-audit/blob/main/page1.html#L12-L13)
- *Problem*: "Java" appears 6 times and "formation" 5 times in two
  sentences, and the heading line is a bare keyword list. This is a
  recognised spam pattern: it is actively penalised, so it hurts more
  than the absence of the keyword would.
- *Fix*: 
    - Rewrite for a human reader. 
    - State the subject once in the `<h1>`, 
    - then describe the course in natural prose. The keyword
  belongs in the title, the `<h1>` and the first paragraph (not
  repeated in every sentence).

#### 8. Thin content (MEDIUM)

- *Where*: [`index.html:17`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L17), [`index.html:25`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L25), [`page1.html:12-13`](https://github.com/ebouchut-laplateforme/seo-audit/blob/main/page1.html#L12-L13)
- *Problem*: each page carries two short sentences of generic text
  (`"Bienvenue sur notre site"`). There is not enough substance for a
  search engine to judge the page relevant to any query, nor for a
  visitor to decide to enrol.
- *Fix*: develop real content: syllabus, duration, prerequisites,
  skills acquired, price, next session dates. Aim for **300 or more words
  of useful text per course page**.

#### 9. Typography of the headline (LOW)

- *Where*: [`index.html:14`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L14)
- *Problem*: `"FORMATION DEVELOPPEUR"` is in full capitals and is
  missing its accent. Capitals are shouting rather than structure — the
  emphasis should come from the markup. What is more `"DEVELOPPEUR"` is a
  misspelling of `"développeur"`, so the correctly accented query matches
  less well.
- *Fix*: `"Formation développeur"`, in an `<h1>`, with the accent.


### Image

#### 10. `<img>` with no `alt` attribute (HIGH)

- *Where*: [`index.html:20`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L20), [`page1.html:9`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/page1.html#L9)
- *Problem*: neither image has alternative text. Search engines cannot
  index the image, screen-reader users get nothing, and nothing is
  shown if the file fails to load. `alt` is also an accessibility
  requirement, not only an SEO one.
- *Fix*: a short, factual `alt` describing the image, for example
  `alt="Développeur travaillant sur une application Java Spring Boot"`.
  Use `alt=""` only for purely decorative images.

#### 11. Non-descriptive image file names (MEDIUM)

- *Where*: `index.html:20` (`IMG_001.jpg`), `page1.html:9`
  (`java-course-final-final2.jpg`)
- *Problem*: 
    - The file name is a ranking signal for image search.
    - `IMG_001.jpg` is a raw camera name and carries none.
    - `java-course-final-final2.jpg` leaks the authoring history.
- *Fix*: rename to lowercase, hyphenated, descriptive names:
  `formation-developpeur.jpg` and `formation-java-spring-boot.jpg`.


### Performance

#### 12. Unoptimised image delivery (MEDIUM)

- *Where*: [`index.html:20`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L20), [`page1.html:9`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/page1.html#L9)
- *Problem*: the `<img>` tags carry no `width`/`height`, so the layout
  shifts while the image loads, which degrades the Cumulative Layout
  Shift metric Lighthouse reports. Both files are JPEG, served at full
  size, with no modern format and no lazy loading.
- *Fix*: set explicit `width` and `height`, serve WebP or AVIF with a
  JPEG fallback via `<picture>`, add `loading="lazy"` to any image
  below the fold, and resize the files to the dimensions actually
  displayed.


### Navigation

#### 13. Non-descriptive anchor text (HIGH)

- *Where*: [`index.html:9`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L9) and [`index.html:32`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L32) (`"Cliquez ici"`),
  [`index.html:10`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L10) (`"Voir"`), [`index.html:28`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L28) (`"En savoir plus"`),
  [`page1.html:16`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/page1.html#L16) (`"Retour"`)
- *Problem*: 
    - Anchor text tells the search engine what the target page is about. 
    - `"Cliquez ici"` describes nothing, so the link passes no
      keyword signal to `page1.html` — and it is unusable for anyone
      navigating link by link with a screen reader.
- *Fix*: name the destination in the link itself: 
    - `"Formation Java Spring Boot"` instead of `"Cliquez ici"`` and `"En savoir plus"`, `"Nos
  formations"` instead of `"Voir"`, `"Retour à l'accueil"` instead of
  `"Retour"`.

#### 14. Broken internal links (HIGH)

- *Where*: [`index.html:10`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L10) and [`index.html:32`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L32) (`page2.html`),
  [`index.html:11`](https://github.com/ebouchut-laplateforme/seo-audit/blob/939c87bb968ebca63b17eb1422f307d628c7f7f6/index.html#L11) (`contact.html`)
- *Problem*: neither target exists in the project, so three of the
  menu links return a 404. Broken links waste crawl budget, break the
  flow of link equity through the site, and are an immediate trust
  signal to a visitor.
- *Fix*: either create the two pages, or remove the links until they
  exist. A site this small should have no 404 reachable from the menu.


### URL

#### 15. Non-descriptive URL (MEDIUM)

- *Where*: `page1.html`
- *Problem*: the URL is itself a ranking signal and is displayed in
  the results. `page1.html` describes nothing, is impossible to guess
  or to share meaningfully, and wastes the keyword opportunity the page
  content already provides.
- *Fix*: 
    - Rename the file to `java-spring-boot.html`, which is also the
      name the brief expects as a deliverable, and update every link
      pointing to it.  
      A 301 redirect from the old URL would preserve any
      acquired ranking — relevant on a live site, not on this lab.
- *Justification for the URL scheme*: lowercase, hyphen-separated
  words, no accents, no underscores, no capital letters, one keyword
  per segment. On a production site the next step would be to drop the
  `.html` extension and group courses under a path that mirrors the
  site structure, such as
  `https://devskills.example/formations/java-spring-boot`.


### SEO technique

#### 16. No `robots.txt` and no `sitemap.xml` (MEDIUM)

- *Where*: project root
- *Problem*: nothing tells a crawler which URLs to visit or to ignore.
  On a small site the pages will probably be found anyway, but
  discovery is slower and you have no control over what gets crawled.
- *Fix*: 
    - Add a `robots.txt` at the root allowing the pages to be crawled
  and pointing to the sitemap, 
    - Add a `sitemap.xml` listing the canonical URL of every page
      with its `lastmod`.

#### 17. No `rel="canonical"` (MEDIUM)

- *Where*: `index.html:2`, `page1.html:2`
- *Problem*: the same content is reachable at several URLs — `/`,
  `/index.html`, and with or without `www` or a query string. Without a
  canonical, search engines may index them as duplicates and split the
  ranking between them.
- *Fix*: `<link rel="canonical" href="...">` in the `<head>` of each
  page, holding the absolute, preferred URL of that page.


## Summary by severity

- **HIGH (7)** — no `<h1>` (1), missing charset (2), duplicate titles
  (5), keyword stuffing (7), missing `alt` (10), non-descriptive anchor
  text (13), broken links (14).
- **MEDIUM (9)** — missing doctype and `lang` (3), no semantic
  landmarks (4), missing meta description (6), thin content (8),
  non-descriptive image names (11), unoptimised images (12),
  non-descriptive URL (15), no `robots.txt`/`sitemap.xml` (16), no
  canonical (17).
- **LOW (1)** — headline typography (9).
