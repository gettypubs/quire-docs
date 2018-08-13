---
title: Figure Images
weight: 205
type: essay
---

Quire books are visual and the framework is built to support the use of images for scholarly purposes. In this page we explain where images are placed in the project and how you can manage them. We recommend using the `figures.yml` file to manage all the information about your images, and then inserting them into your Markdown documents where they are needed with the [`q-figure` shortcode](#inserting-figure-images-with-shortcodes).


## Including Figure Image Files in Your Publication

Figure image files should be placed in the `static/img/` directory. It is defined in your project `config.yml` file with the parameter `imageDir: "/img/"` and the directory can be changed if needed.

[Note] You can organize figures into sub-directories within the `img` folder, but you will need to include those directories along with the filename when defining the `src` attribute for the figure, as noted below.

Quire does not require a specific image file format or size, but we have some recommended best practices:

- Use JPEG, PNG or GIF.
- Only include images at as big a size as most readers will need. 800px on the longest side is fine for most figures, up to 1200px on the longest side for modest zooming. We find these size also work well enough in print.
- Watch out for file sizes, especially on animated gifs which can get to be multiple megabytes quite quickly. Use image optimization[&] software when possible, and consider the total number of images on a given page when choosing sizes.


## Creating a `figures.yml` File for Figure Image Metadata

For most publications, or at least, those with more than just a handful of images, figures and all their associated attributes can be listed in the `figures.yml` file which should be placed in your `data` folder. These then can be called from wherever you need them in your project with a shortcode. See the API-DOCs section for [complete details on possible figure attributes](../api-docs/yaml/#figure), but below there is a very simple example with `id` and `src` (required attributes) and `alt` (recommended attribute).

```yaml
- id: "1.1"
  src: "clyfford-still_untitled96.jpg"
  alt: "detail of painting showing jagged brushstrokes in browns and reds"
- id: "1.2"
  src: "portrait-of-still.jpg"
  alt: "photograph of a frowning older man in brown jacket and fedora"
```

Also available are the attributes `caption`, `credit`, `media_id`, `media_type`, `aspect_ratio`, and `label_text`.

[note] If your figures are organized in sub-directories within your `static/img/` directory, they should appear as part of the file path under `src`, otherwise, only the filename is needed.

## Inserting Figure Images the `q-figure` Shortcode

Assuming each YAML figure entry in the `figures.yml` file includes a unique `id` (with a value in quotes: "1.1" not 1.1), you can insert a figure in your publication with only the `id` attribute in the shortcode, and all of the other attributes defined in the YAML for that figure, will be automatically included.

Figure shortcodes should be inserted on their own line of your Markdown file, not within the text of a paragraph. A basic use of the `q-figure` shortcode would look like this:

```
{{< q-figure id="1.2" >}}
```

If you include an attribute in the shortcode that is also in the `figures.yml` file, the `figures.yml` version is overridden. This can be useful when, for example, a figure is used in multiple locations and you want different captions.

```
{{< q-figure id="1.2" caption="" >}}
```

[note] Note that including an attribute in this way but leaving it blank, as in the caption example above, can also be used to display no caption at all, even if one is present in `figures.yml`.

[note] Also, attributes like `id` and `caption` may be called within the shortcode in any order. `{{< q-figure id="1.2" caption="" >}}` is the same as `{{< q-figure caption="" id="1.2" >}}`.

## Labeling Figure Images

By default, all figure images are labeled automatically, either at the start of the caption, or just under the image itself in the case of a figure group with a single, group caption [(see below)](#creating-and-styling-figure-groups-with-shortcodes). You can turn off this behavior in the `config.yml` file by switching the value `figureLabels: true` to `figureLabels: false`.

Figure labels are constructed  with the `id` of the image and the `figureLabelsTextBefore` `figureLabelsTextAfter` values defined in your `config.yml` file. For example if the `id` value is "12.3" and the `figureLabelsTextBefore` value is "Figure ", and `figureLabelsTextAfter` value is ". ", the resulting label would be "Figure 12.3".

To customize the label text on a figure-by-figure basis, use the `label_text` attribute in the YAML attributes for your figure. Any text there will override the automatically constructed version.

To remove a label from a specific figure or a group of figures, add `label="false"` to the shortcode. Or, in reverse, if you already have `figureLabels: false` set in your `config.yml` file, use `label="true"` in the shortcode to show a label for that figure.


## Styling Figure Images

Depending on your theme[&], by default figures will appear at about the width of the full-column of text. Modifier classes can be added to a shortcode to style the way the figures appear. Available classes are `is-pulled-left`, `is-pulled-right`, `is-large`, and `is-small`. Classes are added just like other attributes in the shortcode.

```
{{< q-figure id="1.2" class="is-pulled-left" >}}
```

![`is-pulled-left-right`](../images/screenshots/left-right.png)


[note]Some themes may offer additional options, and styles may be edited and new styles added in any theme with css[&].

## Creating and Styling Figure Groups with the `q-figure-group` Shortcode

If your project uses a `figures.yml` file, you can also create a group of figures by using the `q-figure-group` shortcode and simply including multiple, comma-separated values in the `id` field.

```
{{< q-figure-group id="1.1, 1.2" >}}
```

In the above example, each figure’s caption will be included in the grouping. Alternatively, if you add a `caption` attribute directly in the shortcode, it will override those present in the `figures.yml` file and display with the group alone as a single, group caption.

![`figure-group-caption`](../images/screenshots/group-caption.png)

Just as with the single `q-figure` shortcode, classes can be added to groups to style them. For example, to create a small group of images running along one side of your text.

```
{{< q-figure-group class="is-pulled-left" id="1.1, 1.2" >}}
```
![`figure-group-caption-left`](../images/figure-group-caption-left.png "The group is positioned on one side of the page")

In addition to all the attributes available to the `q-figure` shortcode, the `q-figure-group` extension also supports the `grid` attribute to specify a preferred grid width. In the below example, a `grid="2"` is specified and so the gallery grid will be 2 images wide at your publication layout’s full-size. Alternately, if you specified `grid="4"` the grid would be 4 images wide making each image relatively smaller.

```
{{< q-figure-group grid="2" id="1.1, 1.2, 1.3, 1.4" >}}
```

![`figures-grid`](../images/screnshots/grid.png)

[note] Note that this is only a **preferred** grid width. With Quire’s responsively designed templates, the specific width of images is variable and their position relative to one another may also change depending on a reader’s device. For instance, on a large monitor, four images in a group may appear side-by-side in a row, whereas on a phone, they would most likely be in a 2 x 2 grid, or stack one on top of another.
This responsiveness also means that group captions that use language like “From left to right” or "Clockwise from upper left," will only be correct some of the time. To avoid this issue and ensure a clear reading experience across all devices and publication formats we recommend labeling figures individually.

## Adding Video Figures

Videos can be embedded in your publication the same way as other figure images, using either of the two figure shortcodes. The difference is in the `figures.yml` file where you’ll need to include a `media_id` and a `media_type` attribute for any video, along with an optional `aspect_ratio` attribute.

Quire supports video embeds from either YouTube (`media_type: youtube`)or Vimeo (`media_type: vimeo`). The `media_id`s can be found in the URLs of the videos you wish to embed. For example, in https://www.youtube.com/watch?v=VYqDpNmnu8I or https://youtu.be/VYqDpNmnu8I, the `media_id` would be `VYqDpNmnu8I`; and in https://vimeo.com/221426899 it is `221426899`.

```yaml
- id: 1.5
  src: videostill.jpg
  media_id: VYqDpNmnu8I
  media_type: youtube
```

[note] The `src` image provided in this example is a frame from the video and will be used in place of the video in the PDF and EPUB versions of your publication. In Quire this is referred to as a fallback. Along with the fallback image, Quire will also automatically append a link to the video following the caption.

Like the [image labels](#labeling-figure-images) this is controlled in the project’s `config.yml` file with `videoFigureFallbackText: true`, `videoFigureFallbackTextBefore: "Watch the video at "` and `videoFigureFallbackTextAfter: "."`.

[note] Note that on YouTube, videos can be filed as “Unlisted” and this will let you embed the video, but will not include the video on your channel page, or in YouTube’s general search engine.

## Adding Basic Figures

If you are not using a `figures.yml` file, figures—including still images and animated gifs but not video—can be inserted in any Markdown document in your publication with the `q-figure` shortcode, where `src` is the name of your file as it appears in the `static/img/` directory of your project.

```
{{< q-figure src="fig01.jpg" >}}
```

Additionally, you can add `caption`, `credit`, `class`, and `id` attributes in this manner.

Unless the figure is purely decorative, it should always also include an alternate textual description (`alt`) for the use of screen readers and other assistive technologies. We recommend using alternate textual description for accessibility purposes. For more information check our [Accessibility Principles](../resources/accessibility-principals/)

```
{{< q-figure src="fig01.jpg" alt="detail of painting showing diagonal brushstrokes in browns and reds" >}}
```
