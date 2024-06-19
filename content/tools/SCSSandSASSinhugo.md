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



