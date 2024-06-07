# Markdown comments

Demonstration of various ways to do Markdown comments.

To try the Markdown yourself: https://babelmark.github.io/

Source: https://stackoverflow.com/questions/4823468/comments-in-markdown


## Markdown comments

If you want a comment that is strictly for yourself (readers of the converted document should not be able to see it, even with "view source") you could (ab)use the link labels (for use with reference style links) that are available in the core Markdown specification:

http://daringfireball.net/projects/markdown/syntax#link



## Text + angles

```markdown
[comment]: <> (alfa bravo)
```

[comment]: <> (alfa bravo)


## Two slashes + angles

```markdown
[//]: <> (alfa bravo)
```

[//]: <> (alfa bravo)

To improve platform compatibility (and to save one keystroke) it is also possible to use # (which is a legitimate hyperlink target) instead of <>:

```markdown
[//]: # (alfa bravo)
```

[//]: # (alfa bravo)

For maximum portability it is important to insert a blank line before and after this type of comments, because some Markdown parsers do not work correctly when definitions brush up against regular text. The most recent research with Babelmark shows that blank lines before and after are both important. Some parsers will output the comment if there is no blank line before, and some parsers will exclude the following line if there is no blank line after.

In general, this approach should work with most Markdown parsers, since it's part of the core specification. (even if the behavior when multiple links are defined, or when a link is defined but never used, is not strictly specified).


## Warning: duplicate link reference

Some markdown parsers emit warnings for multiple links going to the same place.

For example a Pandoc warning looks like this:

```txt
[WARNING] Duplicate link reference '[//]' at example.md line 1 column 1
```

The warning causes problems if such as making a pipline fail when you try to use Pandoc with with the option `--fail-if-warnings`.

 A workaround is to enumerate comments such as:

```markdown
[//1]: # (alfa bravo)
[//2]: # (charlie delta)
[//3]: # (echo foxtrot)
```

[//1]: # (alfa bravo)
[//2]: # (charlie delta)
[//3]: # (echo foxtrot)


## Multiline

In Pandoc this works for multiline comments if there are no blank lines in the commented block (single line breaks are fine). 

```markdown
[//]: # (
    alfa bravo 
    charlie delta
    echo foxtrot
)
```

[//]: # (
    alfa bravo 
    charlie delta
    echo foxtrot
)

Comments:

* Just wanted to note that none of the options listed in this answer worked for this library: github.com/rexxars/react-markdown However, I was able to get it working by replacing the parentheses with quotation marks. 


## HTML comment within a Markdown file

```html
<!--
    alfa bravo
    charlie delta
    echo foxtrot
-->
```

<!--
    alfa bravo
    charlie delta
    echo foxtrot
-->

The Pandoc user's guide says "The raw HTML is passed through unchanged in HTML, S5, Slidy, Slideous, DZSlides, EPUB, Markdown, and Textile output, and suppressed in other formats." 

I tested with pandoc (v2.5). HTML comments are not visible in rendered view. Furthermore current upstream instances of Gitlab and GitHub accepts these.

Please be aware that HTML comments will be part of the HTML document - and thus can be viewed by anyone, e.g. via the right click browser option "view source".


## Pandoc tips

Pandoc has an option `--strip-comments` that will remove all `<!-- comments -->` from the HTML output.
