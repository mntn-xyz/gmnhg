# Links

gmnhg supports links, images, and footnotes. These are extracted from
paragraphs and other block elements recursively.

As there's no inline links in Gemtext, gmnhg instead renders links
blocks after paragraphs. Links blocks are sorted by type: first
footnotes, then images, then links, blocks of a distinct type separated
by a single newline.

## Inline links & images

For inline Markdown links, the text inside the square brackets is used
as link title: for instance, the link to [Gemini specification][gemspec]
along with a link to the current [CommonMark spec][cmark] will generate
a block of two links.

[gemspec]: https://gemini.circumlunar.space/docs/specification.gmi "This alt text will never be printed, as there's no tools in Gemtext for that"
[cmark]: https://spec.commonmark.org/0.30/

[gomarkdown](https://github.com/gomarkdown/markdown) works with
reference-style links as well. Unused reference links are ignored.

[gmnhg]: https://github.com/tdemin/gmnhg "This link will get entirely ignored"

![xkcd #1853](https://imgs.xkcd.com/comics/once_per_day.png) serves
quite well as an inline image example.

Other container elements can contain inline links as well. For instance,
this is an example of a link inside a blockquote:

> OTR has significant usability drawbacks for inter-client mobility.
> — [XEP-0384](https://xmpp.org/extensions/xep-0384.html)

## Footnotes

gmnhg supports footnotes, written like this[^1]. Footnotes can use any
references, including alphanumeric ones[^foo]; alphanumeric references
will be replaced with numeric IDs on render.

[^1]: Footnotes can only consist of a single source line due to a quirk of gomarkdown.
This line looks like it would belong to footnote 1, but it actually
doesn't, and is therefore treated as a new paragraph.

[^foo]: Footnotes can contain any kind of inline **formatting** paragraphs do. For instance, this is a link to [GitHub](https://github.com).

## Lists of links

gmnhg additionally supports a special kind of lists: lists consisting
solely of links. For these, content rendering will be skipped entirely,
and a links block will be rendered instead.

### Markdown lists

Links-only lists can be of any type, but they can only be of level 1.
The two lists below will get rendered as links blocks:

* [Gemini specification][gemspec]
* [gmnhg](https://github.com/tdemin/gmnhg)

1. [Best practices for Gemini implementers](https://gemini.circumlunar.space/docs/best-practices.gmi)
2. [Project Gemini FAQ](https://gemini.circumlunar.space/docs/faq.gmi)

The list below contains other meaningful text in its items, and will get
rendered as a regular list:

* [Gemini specification][gemspec] is a must-read for a Gemini developer.

### Series of links

A series of inline links in a single paragraph, if the paragraph
contains no extra meaningful symbols (aside from spaces and newlines),
will also get rendered as a single links block:

[gmnhg](https://github.com/tdemin/gmnhg)
[Gemini specification][gemspec]

This also works for single-link paragraphs:

[Gemini specification][gemspec]
