---
tags:
  - books
aliases: []
id: book_scanning
---

1. Use `vflat` on your mobile to scan the book as it provides real-time visual feedback. Rescan any blurry pages.
2. Transfer the scanned images to your computer.
3. Use `scantailor` to remove the dirty fringe and output in mixed mode at 400 DPI.
4. Convert tif to jpg using `mogrify -path converted_jpgs -format jpg -quality 20 *.tif`
5. Move the tif files with a file size larger than the corresponding jpg conversions into a list `large tifs`. These files are likely to contain non-binary (color or grayscale) content.
6. Use scantailor to output in black and white mode at 400 DPI. This will reduce file size but result in loss of color information. Fortunately, `large tifs` tells us which tif should contain colors.
7. Replace the black-and-white versions of the files listed in large_tifswith their corresponding color jpg conversions.
8. Merge all images into a pdf using `img2pdf` as it skips unnecessary codec.
9. Apply a searchable OCR layer using `umi-ocr`
