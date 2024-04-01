---
title: SCSS & SASS in Hugo
date: 2023-04-22T06:39:22-07:00
draft: false
---

Create assets/scss/

Files that begin with _ are not meant to be imported into the SASS compiler. They are meant to be used by other scss files.

main.scss file Import other _ files that are in assets/scss:
```
@import "grid";
@import "demo";
```
## Import SCSS or SASS

Add to /layouts/partials/head.html

```
<title>{{ .Title }}</title>
{{ $css := resources.Get "scss/main.scss" }}
{{ $css = $css | toCSS }}

<link rel="stylesheet" href="{{ $css.RelPermalink}}">
```



