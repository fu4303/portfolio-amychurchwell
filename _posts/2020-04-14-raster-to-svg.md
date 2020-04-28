---
layout: post
title:  "Convert a raster image to svg in photoshop"
categories: tech
tags: photoshop
---

Hello! While this has probably been written about before, it's a common issue I encounter when working with assets on websites-- so I thought: _what the heck, I'll write a quick tutorial..._

---

### What is an SVG? Why do we care?
For the sake of keeping this post brief & to the point, all you need to know moving forward is that [**Raster image formats**](https://en.wikipedia.org/wiki/Raster_graphics) (such as **JPG** and **PNG**) are created with a set amount of colored pixels. If you have seen an image on the web that is blurry, it is because this image format is sized beyond it's resolution and those square colored pixels that compose the image are now visible.

**SVG** does not have this resizing issue because it renders graphics in a fundamentally different way- [using code to describe shapes and paths!](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Basic_Shapes) _whaattt? crazy!_ [Learn more here.](https://developer.mozilla.org/en-US/docs/Web/SVG)

---

## In this tutorial, we will take a **raster JPG image** and convert it to an **SVG** using Photoshop.

**NOTE: This method works best on images that have easily separated colors and good contrast. (For example: icons, simple line drawings, logos, text, .etc.)**


Here is the raster graphic we will use for this example. I doodled it in about 5 seconds in Photoshop using the brush tool.
![screenshot](/assets/img/posts/JPG-SVG/cat.jpg)

## 1. Open the image in Photoshop. On the top toolbar, go to: **Select** > **Color Range**
You can use the eyedropper tool to isolate a single color in your image and tweak the **Fuzziness** slider until the preview is your desired selection.

![screenshot](/assets/img/posts/JPG-SVG/screenshot1.png)

## 2. Right click and select **Make Work Path**. A dialog will appear asking about **Tolerance.**
![screenshot](/assets/img/posts/JPG-SVG/screenshot2.png)

**Question:** What is a work path?

**Answer:** A **work path** is a vector shape made of a series of anchor points. 

**Question:** What is tolerance?

**Answer:** In Photoshop, **tolerance** essentially means the sensitivity of a tool. In our case, the higher the tolerance the looser the work paths tracing our selection will be because it will have fewer anchor points.

### What tolerance should I pick? (Depends on the image!)

| Filled Work Paths | Tolerance Setting |
| ------------- |-------------|
|![screenshot](/assets/img/posts/JPG-SVG/tolerance0.5.svg)| **0.5** |
|![screenshot](/assets/img/posts/JPG-SVG/tolerance1.svg)| **1** |
|![screenshot](/assets/img/posts/JPG-SVG/tolerance1.5.svg)| **1.5**|

As we can see, it is never quite a _perfect_ match but Photoshop tries it's best. If you'd like to clean up the jagged edges you can use the **pen tool** to tweak the anchor points.

**TIP:** To avoid this issue, make your SVG larger than the size you'd like to use in production. It will seem crisper at a smaller size. See [How to scale SVG](https://css-tricks.com/scale-svg/) by Amelia Bellamy-Royds.

## 3. Create a new fill layer. **Layer** > **New Fill Layer** > **Solid Color**
It will ask for a color, black is easiest to work with in my experience.
![screenshot](/assets/img/posts/JPG-SVG/screenshot3.png)

After creating your fill layer you can delete the original layer to see your work.
![screenshot](/assets/img/posts/JPG-SVG/screenshot4.png)

## 3. Export as SVG. **File** > **Export** > **Export As...**
![screenshot](/assets/img/posts/JPG-SVG/screenshot5.png)
![screenshot](/assets/img/posts/JPG-SVG/screenshot6.png)

## 4. Optimize!

If you open your newly created SVG in a text editor, you might notice a lot of extra information. Things not related to the drawing of the image, like `<metadata>` or XML instructions. Removing this extra information not only simplifies the code but makes the file size smaller. _woo hoo!_

One of my favorite tools for removing all the cruft in SVG's is [SVGOMG](https://jakearchibald.github.io/svgomg/) by Jake Archibald, which is a very nifty GUI utilizing [SVGO](https://github.com/svg/svgo). You can upload your image or paste your markup in the tool and it will strip out all unnecessary data.

## 5. Enjoy working with SVG's!

<figure>
    <svg xmlns="http://www.w3.org/2000/svg" width="243" height="249.469">
        <defs>
            <style type="text/css"><![CDATA[
            #cat {
                fill: RebeccaPurple;
            }
            ]]></style>
        </defs>
        <path id="cat" d="M163 58c18.126.5 31.036-6.146 40-15 1.754.631.971.193 2 1 1.938 1.667 1.668 1.439 2 5-13.965 6.625-19.01 14.883-41 15 .423 7.611 4.857 17.779 2 27-.816 2.635-3.113 5.678-4 9h13c11.454-7.255 17.9-1.143 26-15-10.114-10.12 1.8-21.23 7-26a67.543 67.543 0 0118 2l7 8c-.143 10.568-5.317 9.807-8 16-2.073 4.784.736 11.82-1 16-7.357 17.715-29.935 23.709-51 28v4c2.455 3.7 3.053 12.479 4 17 3.669 1.791 6.736 5.468 10 7 5.007 2.351 9.587 1.386 14 4 3.568 2.114 4.8 4.949 10 6 5.294-7.22 16.5-6.384 26-4 2.615 5 4.1 7.26 4 16-7.622 9.978-8.987 21.147-27 21-2.947-2.194-33.055-12.616-38-11-3.535 1.155-7.775 7.359-9 11 15.459.138 17.048 10.214 28 14 5.567-5.551 15.035-4.972 23-3 4.008 15.955-7.06 25.766-20 31-2.841 1.149-9.958 3.688-14 1-5.617-2.057-8.194-8.14-14-10-21.443-6.869-39.793 11.915-64 6-2.736-.669-7.494-3.641-10-4-2.7-.387-2.057 1.607-4 2H56c-13.209 2.938-23.713 8.9-35 12-3.637 1-11.95.248-14-1-4.839-1.512-6.728-4.889-7-11 5.094-6.41 7.824-13.749 15-18 14.1-8.353 42.958-3.175 63-3v-1c-12.236-13.088-7.086-54.864-7-79h-2v-1l-1 1c-10.947 6.962-15.686 18.518-24 28-1.754-.631-.971-.193-2-1-2.521-1.462-1.828-1.255-2-5 1.245-.971 19.6-24.884 20-26a16.623 16.623 0 01-12-8c-11.559 5.94-19.265 21.473-34 23v-2c-.752-1.073-.6-.946-1-3 8.177-4.965 24.92-16.423 30-24-2.985-2.471-2.837-5.448-7-7-5.166 4.069-18.818 8.189-26 9-1.121-2.091-1.434-1.832-2-5 5.726-3.043 25.813-7.841 28-13-4.412-5.945-.6-18.557-1-26-.917-17.274.9-55.451 16-57 3.2 4.982 23.705 27.937 29 29 3.206-2.118 10.091-1.7 14-3-.42-13.452 5.2-43.93 16-45l19 19c3.591 4.782 5.933 10.655 10 15 1.724 1.842 11 4 11 4 5.58-6.077 8.011-19.879 10-29a15.7 15.7 0 015-1c.961 1.766 1.257 1.68 2 4-2.188 2.891-10.349 28.573-11 33l2 2c1.754-.631.971-.193 2-1 10.769-3.711 15.214-16.993 28-18 .631 1.754.193.971 1 2-.631 1.754-.193.971-1 2-3.717 7.873-18.171 17.091-26 21l1 5zM108 9c-3.063 12.383-6.846 23.412-7 40-3.086 1.947-3.43 2.886-9 3-3.711 2.389-12.985 2.836-18 3-6.635-10.165-17.4-17.116-24-27l-1 1c-6.87 7.6-8 27.933-8 43 0 50.7 11.418 58.1 62 58 9.511-.019 16.063-1.061 23-4 22.879-9.694 45.094-36.266 31-68-2.724-6.134-8.822-13.227-15-16-2.487-1.117-5.151-.345-7-2-2.785-2.492-3.755-6.884-6-10zm4 18l5 1c1.19 4.528 2.792 5.814 3 12-1.766.962-1.68 1.257-4 2-1.18-.8-1.681-.773-4-1-1.316-3.564-1.279-10.436 0-14zM51 47h4c3.392 6.029 7.7 10 8 19-4.546 2.66-5.2 2.379-12 2-1.712-4.753-1.675-16.245 0-21zm69 12c7.442 1.435 8.487 4.671 8 14-2.2 1.664-2.026 2.836-5 4-1.992 1.337-6.507 1.1-10 1-1.833-3.426-2.115-8.028-2-14 .8-1.021.355-.274 1-2 1.688-.838 6.211-1.774 8-3zm-43 78c-.492 47.7-3.318 86.715 35 96 23.763 5.758 34.858-13.667 60-7 9.134 2.422 12.069 11.331 22 12 8.775-6.548 19.055-7.578 21-21a25.086 25.086 0 00-8-1 26.278 26.278 0 01-12 5c-2.321-1.838-5.536-2.227-8-4l-9-9-19-3c-.877-1.295-.894-2.467-1-5l18-18c19.106-.023 29.424 10.447 48 11 5.508-8 12.053-8.457 12-23-3.426-1.833-8.028-2.115-14-2-3.884 4.311-7.828 6.457-14 6-7.591-9.377-29.365-9.447-34-21-4.416-4.885-5.833-18.54-6-27 17.637-9.792 40.552-9.012 51-26 3.058-4.972-.776-12.675 2-19 1.98-4.512 6.322-3.531 7-11a24.935 24.935 0 01-5-4h-12c-1.283 2.072-2.077 2.3-3 5-4.034 5.155.6 10.375 1 18-14.917 14.142-20.194 17.143-50 17-13.224 26.438-41.367 31.156-82 31zm-7-62l10 1c3.267 5.373 7.552 7.65 8 16-1.754.631-.971.193-2 1-1.754-.631-.971-.193-2-1-6.422-3.333-3.733-9.67-14-10-2.413 3.846-3.141 6.82-3 14-2.091 1.121-1.832 1.434-5 2-1.833-3.426-2.115-8.028-2-14 2.665-2.867 2.716-5.487 7-7 .771-.682 2.232-1.311 3-2zm33 10c3.915 1.071 3.838 1.141 4 6l-3 1c-1.3.877-2.467.894-5 1a15.7 15.7 0 01-1-5 17.263 17.263 0 005-3zm19 3h7c1.782 3.043 2.781 3.841 3 9-5.689 6.315-5.946 15.9-15 19-7.343 5.532-20.211 1.95-28 0-1.947-3.086-2.887-3.43-3-9 11.819-6.39 26.021-10.629 36-19zm-30 64h5c1.742 5.123 1.078 14.248 1 21 7.185 10.985-1.575 19.206-2 29 4.721 1.245 6.334 2.873 13 3 3.508-5.134 6.913-5.826 7-15l-8-4c-1.049-8.446-1.67-21.6 0-30a14.124 14.124 0 014-1c2.969 5.649 2.123 17.288 2 26 4.235 1.953 5.954 4.106 9 7 .331 15.178-5.628 17.1-13 24-14.157.52-21.663-4.058-21-19 8.3-7.733.376-26.214 3-41zm-65 70c-2.87 2.024-7 2.03-10 4-4.026 2.645-6.549 7.7-10 11l1 5h13c12.744-11.788 41.988-11.957 67-12v-1c-2.441-2.381-3.678-5.45-7-7-4.759 3.016-44.35.123-54 0z" fill-rule="evenodd"/>
    </svg>

</figure>

```css
svg {
    fill: RebeccaPurple;
}
```

More tips about working with SVG's:

- [SVG Will Save Us](https://youtu.be/sxte3WpyO60) by [Sarah Drasner](https://sarahdrasnerdesign.com/)
- [Getting Started with SVG](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial) by [Mozilla Developer Network](https://developer.mozilla.org/).
