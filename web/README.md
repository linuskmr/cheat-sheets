# Web best practices tools

## Lighthouse Chrome DevTools

[Lighthouse](https://developers.google.com/web/tools/lighthouse) inside the Chrome DevTools analyzes
a web page and generates a report of how to improve a website. This includes:

* Next-gen image formats (AVIF, WebP)
* Image size
* Lazy image loading
* Cache policy

## Mozilla Observatory

[Mozilla Observatory](https://observatory.mozilla.org) analyzes a web page for potential security risks. This includes:

* Content Security Policy
* Cookies
* Cross-origin Resource Sharing (CORS)
* XSS-Protection Header

## HTML Tags

header, nav, main, p, a, article, section, figure (image with caption), picture (multiple sources), datetime, del & ins (delete and newly inserted text), abbr (Abbreviation)

input enterkeykint: enter, done, go, next, previous, search, send

blockquote: `cite` attribure as source of citation

img: `loading="lazy"`

`del` & `ins` can have `cite` and `datetime` attributes

`select` → `optgroup`: `label=Text` to seperate options in a long select list

script `integrity=some-hash...`
