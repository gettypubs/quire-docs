---
title: Markdown
weight: 301
type: essay
---
Markdown is a very simple, plain text markup language that uses a few text rules to structure content for easy conversion into HTML. Writing in Markdown should be thought of as giving your content structure, not style. By design, and through the stylesheets in the project theme, a list or a blockquote might look different from theme to theme, or even from format to format.

## Basic Markdown Tags

Here are the most commonly used tags:

```
*Italic Text*
**Bold Text**
```
*Italic Text*

**Bold Text**

```
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
```
# Heading 1
## Heading 2
### Heading 3
#### Heading 4

On the headings, in general you should not use the *Heading 1* tag in your content as that should be reserved for the page title, which is automatically generated. Start with *Heading 2*. Also headings should be thought of as levels of your content outline, not as sizes large to small, though they’re often thought of and used that way. See our [*Notes on accessibility*](../resources/accessibility.md) for more on this.

```
> Blockquote
```
> Blockquote

Links are created with text in brackets followed immediately by a url in parentheses:

```
[Link Text](http://www.linkadress.com)
```
[Link Text](http://www.linkadress.com)


```
- dashes make
  - a list with
    - bullets
```
- dashes make
  - a list with
    - bullets

```
* asterisks make
  * a list with
      * bullets
```

* asterisks make
  * a list with
      * bullets

Indented dashes and asterisks create sub bullets in a bulleted list.

```
1. numbers make
2. a list with
3. numbers
```

1. numbers make
2. a list with
3. numbers

## Markdown Formatting Gotchas

- Individual paragraphs are created with double line breaks.

- Special characters like en- and em-dashes, and diacritics also work fine in Markdown and in Quire publications. Any Unicode character is allowed, the only limitation, for less common characters, is whether the font you’re using includes it. When a font does not include a specific character, most browsers will substitute one from a different font.

- &#40;c&#41; will automatically render as ©.

- You can also use HTML tags in a Markdown file. This can be convenient for adding HTML elements that Markdown doesn’t support, or for applying special styling. For instance, by wrapping text with a `<span>` tag with a class in order to add custom styling. (See more about this in the [*Customizing Styles*](../styles.md) chapter of this guide.) Note, however, that you can’t do the same by wrapping multiple paragraphs of Markdown in `<div>`, `<section>` or other block-level tags. For this, you need the `q-class` shortcode. Read more about Quire shortcodes below.

## Markdown Footnotes

Footnotes can also be added with Markdown. Use a numbered marker like `[^1]` in the text where you want the number to go, and then at the end of the page, usually under a “Notes” heading, add the corresponding footnote:

```
## Notes

[^1]: The footnote itself is the same thing as the footnote number reference in the text, but with a colon followed by the footnote text
```

Footnotes can also include Markdown formatting, including lists and even multiple paragraphs. For these, indent the content inwards two levels and put a line space in between the paragraphs just as you would elsewhere.

```
## Notes

[^2]:
    Footnotes with multiple paragraphs

    Are indented in twice, and have line breaks between.

    - Markdown lists
    - work like this in footnotes
    - as well
```

[note/warning] The built-in Markdown processor[&] will automatically renumber footnotes in the order they appear in the text. It will also always put the footnotes at the very end of your content, no matter where you may try to put them.

[note/warning] Blackfriday[&], the built in Markdown processor, will incorrectly also create link even if there is a space between the bracketed text and the parentheses. For instance, a footnote reference number `[^1]` followed by a space and any text in parentheses, will incorrectly format as a link: `[^1] (Some aside text here)`. To avoid this, you can use the HTML entity reference, `&#40;`, for the first parentheses, or a backslash escape character before the first parentheses:

```markdown
[^1] &#40;Some aside text here)
[^1] \(Some aside text here)
```

## Fractions, Superscripts and Subscripts

The fractions 1&#47;4, 1&#47;2, and 3&#47;4, will be automatically converted into proper, Unicode fractions (1/4, 1/2, 3/4). Other Unicode fractions can also be used in Markdown directly, though note that not all fonts support the eighths in which case, browsers will render them with a default font. The fractions are: ¼, ½, ¾, ⅛, ⅜, ⅝, ⅞. Any others would need to be written using superscript and subscript formatting.

While some Markdown processors[&] support superscript and subscript formatting with ^ and ~ characters, the one built into Quire does not. You’ll need to use the HTML `<sup>` and `<sub>` tags in your Markdown. For example:

- `19 × 24<sup>3</sup>⁄<sub>16</sub> inches` = 19 × 24<sup>3</sup>⁄<sub>16</sub> inches
- `20<sup>th</sup> Century Sculpture` = 20<sup>th</sup> Century Sculpture
- `Chrome yellow (PbCrO<sub>4</sub>)` = Chrome yellow (PbCrO<sub>4</sub>)

You will see a `fractions` attribute with a value of "false" in the `config.yml` file of your publication. Changing this to true will automatically render fraction-style superscript and subscript formatting for anything written as an integer followed by a slash and another integer. However, in many instances this will catch things that are not meant to be fractions. For this reason, we recommend leaving `fractions` set to `false`, and manually adding the necessary markup as it’s needed.

## Markdown Preview

Many text editors offer a preview function for Markdown, either pre-installed or as an add-on. In Atom for instance, a Markdown file can be previewed by selecting Packages > Markdown Preview > Toggle Preview (or just Shift-Control-M). The preview won’t match the style of your publication site, but will have default styling for headings, blockquotes, links and the like to allow you to confirm proper formatting.

Outside of more code-driven text editors, there are also a growing number of Markdown-specific editors. [Typora](https://typora.io/), for instance, offers a single-page live preview by displaying styled Markdown-formatted text as you type it.

## Markdown Output Configuration

Hugo has a built-in Markdown processor, Blackfriday[&](https://github.com/russross/blackfriday), which comes with some configuration options that can be applied in your project’s `config.yml` file. Details can be found [in the Hugo documentation](https://gohugo.io/getting-started/configuration/#configure-blackfriday).

By default, in the `config.yml` file of your Quire project, Blackfriday’s[&] `fraction` option has been set to `false` (text that looks like a fraction won’t be automatically formatted as such.), and the `hrefTargetBlank` option set to `true` (external links will open in new windows/tabs).

## Markdown Resources

This guide doesn’t cover all existing Markdown tags but there are some good sources that will help you find the right syntax to format your text. For example, the Programming Historian provides an [introductory lesson to Markdown](https://programminghistorian.org/lessons/getting-started-with-markdown), and John Gruber, the creator of Markdown, provides a comprehensive explanation of the basics and syntax on his personal site [Daring Fireball](https://daringfireball.net/projects/markdown/).

Be aware of the multiple [Markdown flavors](https://github.com/commonmark/CommonMark/wiki/Markdown-Flavors) out there and the fact that not all flavors are supported by Blackfriday[&].

## Microsoft Word to Markdown Conversion

Commonly, project content will start from Microsoft Word documents rather than being written originally in Markdown. In these cases, a simple file conversion using Pandoc[&] can be done.

There are some easy things you can do in the Word document prior to conversion to ensure the best possible results:

- We recommend not to insert any images and media to the Word document before conversion.
- Headings must be formatted with Word styles instead of by changing font formats.
-

While there are a number of free tools, we recommend using Pandoc[&]. You can find installation instructions on their site.

Once installed, make sure you are in the folder where your .docx document is saved, and enter the Pandoc command on the command-line application. The command used to convert your file is: `pandoc -s your_document_name.docx -t markdown -o your_document_name.md`. However, in order to optimize the default conversion you should specify the following extensions:

- Quire needs ATX-style Markdown headers[&], these are specified adding `--atx-headers` to the command.
- The lines of the generated Markdown file[&] are 80 characters long. Adding the option `--wrap=none` to the command will override the default wrapping making easier to work with your files in the text editor[&].

The order of the extensions doesn't matter, and you can either type: `pandoc --atx-header --wrap=none -s your_document_name.docx -t markdown -o your_document_name.md` or `pandoc -s your_document_name.docx -t markdown --atx-header --wrap=none -o your_document_name.md`
