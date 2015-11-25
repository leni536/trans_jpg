# trans_jpg

This little experiment makes use of SVG's image and mask elements and data URIs to create transparent images. Both the color and transparency layers are stored as separate jpeg images embedded inside the svg file as data URIs. This kind of SVG file structure is quite simple:

```svg
<svg xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink" width="240" height="240">
  <defs>
    <mask id="Mask" width="240" height="240">
      <image id="alpha" width="240" height="240"
         xlink:href="<mask jpeg's data URI>" />
    </mask>
  </defs>

  <image width="240" height="240" mask="url(#Mask)"
     xlink:href="<jpeg's data URI>" />
</svg>
```

The result:

https://github.com/leni536/trans_jpg/blob/master/trans_jpg.svg

size considerations
===

Obviously my sample image is not really a good candidate for this experiment so especially bad for benchmarking. Anyway:

| | jpegs | svg          |
| ------ | -------: | -----------: |
| raw | 8262 |  11543 |
| gzip -9 | 6607 | 7142 |

This is ~8% larger than the source jpg files for the gzipped version (you may want to gzip svg files anyway on your server). This is without any attempt to minify the SVG template by hand which could save a few bytes.

Notes
===

One can mix different type of images this way, like using jpg for the color layers but using png for transparency. In certain cases this can be smaller than a transparent png image with many colors without visible difference.
