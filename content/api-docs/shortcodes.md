---
title: Shortcodes
type: essay
---

## `q-backmatter`

Sample: `{{< q-backmatter >}}The text you want formatted here.{{< /q-backmatter >}}`

Basic Usage: Wrapping text in this shortcode will format it in a manner similar to how footnotes and bibliographies are formatted. Good for sections at the end of essays like Appendices, Acknowledgments, and Contributors Bios.

Parameters: None.

YAML Dependencies: None.

See: [Working with Text](../guide/pages-plain-text)

## `q-bibliography`

Basic Usage: Generates a bibiliography from the entries in the project's `bibiliography.yml` file.

See: [Citations & Bibliographies](../guide/citation-bibliographies)

## `q-cite`

Basic Usage: Adds a linked Author Date citation reference to the text, and a hover pop-up with the full citation text. It also adds the citation to a map of cited works, which can then be output as a page-level bibliography on essay and entry type pages.

See: [Citations & Bibliographies](../guide/citation-bibliographies)

## `q-contributor`

Sample: `{{< q-contributor range="page" type="bio" >}}`

Basic Usage: Can be used to create a page of contributor biographies, a section of bios for a single page, a simple list of contributors, a byline for a particular page, or other similar outputs.

Required Named Parameters: "range" and "type"

### type

| Expected Value | Description                              |
| -------------- | ---------------------------------------- |
| "initials"     | Looks for the capital letters in a contributor first and last name and concatenates them together. |
| "name"         | Just the first and last name.            |
| "name-plus"    | The first and last name with, when available, their title and affiliation on a line below. |
| "bio"          | First and last name, with pic, url, and bio as available. Plus a link to their contribution. |

### range

| Expected Value     | YAML Location                            | Description                              |
| ------------------ | ---------------------------------------- | ---------------------------------------- |
| "page"             | `.Page.Params.contributor`               | In the current Page under `contributor`  |
| "essays"           | `.Site.Pages.Params.contributor`         | In any Page with a `type: essay` under `contributor` |
| "all"              | `.Site.Pages.Params.contributor`         | In all Pages under `contributor`         |
| "primary"          | `.Site.Data.publication.contributor` with a `type` of "primary" | In `publication.yml` under `contributor` |
| "secondary"        | `.Site.Data.publication.contributor` with a `type` of "secondary" | In `publication.yml` under `contributor` |
| "project-team" | `.Site.Data.publication.contributor` with a `type` of "project-team" | In `publication.yml` under `contributor` |

YAML Structure:

| YAML Attribute | Required | Notes
| --- | --- | --- |
| Either both `first_name` and `last_name`, OR `full_name` | Y | If all are included, `full_name` will override the others. |
| `title` | N |  |
| `affiliation` | N |  |
| `role` | N | When the shortcode range is "publication-team", `role` is used in place of `title` |
| `bio` | N | Markdown okay |
| `url` | N |  |
| `pic` | N | Filename only. File must be in the top level image director, or in a sub-directory defined in `config.yml` with `contributorSubDir`. |

See: [Contributors](../guide/contributors)

## `q-copyright`

Sample: `{{< q-copyright >}}`

Basic Usage: Adds a copyright statement and licensing information as you’ve defined it in your `publication.yml` file. Commonly used on Copyright and About pages. The shortcode itself makes use of the `copyright.html` partial in your site templates.

Parameters: None.

See: [Copyright & About Pages](../guide/copyright-about-pages)

## `q-figure`

Sample: `{{< q-figure id="3.1" >}}`

Basic Usage: Inserts a formatted figure image, label, caption and credit line. If using a `data/figures.yml` file, only an `id` parameter is required for this shortcode. If other values supplied directly in the shortcode they will override any corresponding values in the `data/figures.yml`.


| Named Parameters | Expected Value  | Description |
| --- | --- | --- |
|`id` | string | Spaces or special characters should not be used and will be stripped out. When used in a shortcode *without* a corresponding `src` parameter, the shortcode will look for a matching `id` in the project’s `data/figures.yml` file. When used in a shortcode *with* a corresponding `src` parameter, this will create an `id` for the image markup that can be used to link to the image directly (`mypublication.com/chapter01/#fig-3`) and ignores any  potentially corresponding information in the `data/figures.yml` file. |
| `src` | url | Should be the file name of a JPG, PNG or GIF image (`fig01.jpg`). Avoid using spaces or special characters, and if it’s in a sub-folder within the main `img` directory (which is defined by the `imageDir` parameter in the `config.yml` file), it should include that sub-folder name as well (`comparatives/fig01.jpg`). If your project uses `data/figures.yml` file, you shouldn’t use a `src` parameter in the shortcode as it will override all other information.  |
| `alt` | string | For accessibility, all images should have alternative text descriptions. ([Tips on crafting good alt text.](https://webaim.org/techniques/alttext/)) Only ever leave blank if the image is purely decorative. |
| `caption` | string | The caption to appear below the figure. Special characters are allowed. Use Markdown for formatting. |
| `credit` | string | Follows the caption. Markdown allowed. |
| `label` | boolean | Default is set to `true`. `true` will add a label to the caption, such as "Figure 1.3", `false` will remove the label. The global label setting is in the `config.yml` file under the parameter `figureLabels`.  |
| `label_text` | string | Will override the default label text for the figure, which is otherwise constructed automatically with the `figureLabelsTextBefore` and `figureLabelsTextAfter` parameters in `config.yml`. |
| `class` | `is-pulled-right`, `is-pulled-left`, `is-full-width`, `is-centered-small` | Sets the style of the figure image. |

See: [Figure Images](../guide/figure-images) and [Figure YAML](#)

## `q-figure-group`

Sample: `{{< q-figure-group id="3.1, 3.2, 3.3" >}}`

Basic Usage: Like `q-figure`, but with handling for multiple images at once.

| Named Parameters | Expected Value  | Description |
| --- | --- | --- |
|`id` | string | One or more comma-separated `id`s that match corresponding values in the project’s `data/figures.yml` file. |
| `caption` | string | The caption to appear below the figure group. Special characters are allowed. Use Markdown for formatting. Overrides any caption information provided in `data/figures.yml`. |
| `credit` | string | Follows the caption. Markdown allowed. Overrides any caption information provided in `data/figures.yml`. |
| `label` | boolean | Default is set to `true`. `true` will add a label to the caption, such as "Figure 1.3", `false` will remove the label. The global label setting is in the `config.yml` file under the parameter `figureLabels`. If a `caption` is also provided in the shortcode, the labels will be applied on their own directly under each image in the group, rather than as part of the caption. |
| `class` | `is-pulled-right`, `is-pulled-left`, `is-full-width`, `is-centered-small` | Sets the style of the group of figures overall. |
| `grid` |  `1`, `2`, `3`, `4`, `5`, `6` | Determines the horizontal width (in number of images) of the image grid. If no grid is set, the images will stack on top of one another vertically. |

See: [Figure Images](../guide/figure-images) and [Figure YAML](#)

## `q-link-list`

Sample: `{{< q-link-list "other-formats" >}}`

Basic Usage: Creates an unordered list of links. Makes use of the `link-list.html` partial in the site templates.

Parameters:

| Parameter Position | Expected Value                       | Description                              |
| ------------------ | ------------------------------------ | ---------------------------------------- |
| 0 *                | "other-formats", "related-resources" | Values point to corresponding values in `publication.yml` |

Parameters are not named, but instead defined by their position, starting at 0.

See: [Copyright & About Pages](../guide/copyright-about-pages)

## `q-loc`

Sample: `{{< q-loc >}}`

Basic Usage: Adds formatted Library of Congress Cataloging-in-Publication Data to the page, from values in `publication.yml`.

Parameters: None

See: [Copyright & About Pages](../guide/copyright-about-pages)

## `q-publisher-team`

Note: this should be folded into the `q-contributor`.

## `q-revision-history`

Sample: `{{< q-revision-history >}}`

Basic Usage: Adds a revision history to the page, based on values in `publication.yml`.

| Named Parameters | Expected Value  | Description                              |
| ---------------- | --------------- | ---------------------------------------- |
| format           | "short", "full" | "short" will show only the first publication date and most recently updated date. "long" shows all dates and list of changes for each. |

See: [Copyright & About Pages](../guide/copyright-about-pages)

## `q-table`

Note: Original version of this was tabled. Still looking for better solution for complex tables.

See: [Figures](../guide/figure-images)

## `q-url-link`

Note: Not sure we‘ll do this. Might be better to build in with JS rather than have a separate shortcode just for URLs.

See: [Working with Text](../guide/pages-plain-text)
