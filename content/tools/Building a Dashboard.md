https://www.youtube.com/watch?v=AatZl1Z_n-g&list=PL7oLu8NfQd84_gsyqBVSVgUmCCgcvSZMx&index=22
Settings > appearance > CSS Snippets > folder icon
https://github.com/TfTHacker/DashboardPlusPlus
https://github.com/TfTHacker/DashboardPlusPlus/blob/master/.obsidian/snippets/dashboard.css

```
/* Updated 2022-02-28 */

.dashboard {

padding-left: 25px !important;

padding-right: 25px !important;

padding-top: 20px !important;

}

.dashboard .markdown-preview-section {

max-width: 100%;

}

/* Title at top of the document */

.dashboard .markdown-preview-section .title {

top: 60px;

position: absolute;

font-size: 26pt !important;

font-weight: bolder;

letter-spacing: 8px;

}

.dashboard h1 {

border-bottom-style: dotted !important;

border-width: 1px !important;

padding-bottom: 3px !important;

}

.dashboard div > ul {

list-style: none;

display: flex;

column-gap: 50px;

flex-flow: row wrap;

}

.dashboard div > ul > li {

min-width: 250px;

width: 15%;

}
```

Paste into notepad > save as dashboard.css > add to snippets folder in .obsidian
enable the snippet.

Create a new page called home

add cssclass: dashboard to the [[YAML In Obsidian]] header.

Grab the dashboard++ markdown file from the repo

See video at 3:32 to turn readable line length on for only this page (if needed)

* Each list expands to the right

### Add a Banner

add banners plugin > create page called banners > drag and drop image file into their > open commands on page and type "banner" > select add from local image

can change banner height from the plugin

install homepage plugin
Opens obsidiann in homepage
set homepage > set homepage view to "reading view" > turn on "refresh dataview"
set up homepage hotkey to ctrl+h