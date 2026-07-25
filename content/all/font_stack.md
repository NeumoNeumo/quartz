---
id: font_stack
aliases: []
tags: []
---

## Rendering pipeline
- fontconfig: selects a font face based on family / lang / charset / weight, etc.
- FreeType: opens the font file and reads glyph outlines, bitmaps, and metrics
- HarfBuzz: performs shaping based on font tables and outputs the final glyph sequence and positions
- FreeType: loads and rasterizes specific glyphs

Example:
```C
FcPattern *pat = FcPatternCreate();

FcPatternAddString(pat, FC_FAMILY, (FcChar8 *)"serif");
FcPatternAddString(pat, FC_LANG,   (FcChar8 *)"zh-cn");
FcCharSetAddChar(cs, 0x4F60); // 你
FcCharSetAddChar(cs, 0x597D); // 好
FcPatternAddDouble(pat, FC_SIZE, 16.0);

FcConfigSubstitute(NULL, pat, FcMatchPattern);
FcDefaultSubstitute(pat);

FcResult result;
FcPattern *match = FcFontMatch(NULL, pat, &result);k

FcChar8 *file = NULL;
int index = 0;

FcPatternGetString(match, FC_FILE, 0, &file);
FcPatternGetInteger(match, FC_INDEX, 0, &index);

FT_New_Face(ft_library, (const char *)file, index, &face);
```

## Basic concepts

- font family: e.g. Noto Serif CJK SC
- font face: e.g. Noto Serif CJK SC Bold
- ttf file: a single-font file. Typically contains:
    - Character mapping(cmap): Unicode codepoint -> glyph ID
    - Glyph data: glyph ID -> outline / bitmap / color layers
    - Metrics: how the glyph occupies space and is positioned.
- ttc file: a font collection. Useful in CJK since there a lot of overlapping
- em square: the font designer’s abstract design box for one nominal font size.
- glyph bounding box: actual outline area of a specific glyph.
- advance width: horizontal space reserved before the next glyph. = left side bearing + right size bearning + glyph bounding box width
- OpenType: a font container format supporting different glyph descriptions like quadratic Bézier vector outlines and embedded bitmap images. OpenType fonts with different outline formats have different extensions. For example, `.ttf` represents OpenType font with TrueType outlines in the `glyf` table and `.otf` is that with CFF/PostScript outlines in the `CFF` or `CFF2` table.

> [!Info]- TrueType vs CFF
> TrueType is older and uses quadratic Bézier curves while CFF uses cubic Bézier curves which makes it more controllable and welcomed among designers. CFF is also more compact then TrueType. [^1]

FC_CHARSET mainly comes from cmap, while FC_LANG mainly comes from FC_CHARSET + fontconfig’s built-in language rules.

If a glyph is missing in a font, the program might deal with it with a fallback font. If it doesn't handle it, you will see a tofu.

Glyphs for the same character at the same FC_SIZE in different fonts may appear to have different visual sizes because FC_SIZE only determine the scale of the em square in design but the designer is free to decide how much of that em square each glyph occupies.

## Reference

- https://catcat.cc/post/2020-10-31/
- https://catcat.cc/post/2021-03-07/
- [异体字测试](https://catcat.cc/raw/fontconfig.html)
- https://fontconfig.pages.freedesktop.org/fontconfig/fontconfig-user.html
[^1]: https://blog.typekit.com/2010/12/02/the-benefits-of-opentypecff-over-truetype/

