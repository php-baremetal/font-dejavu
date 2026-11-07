# font-dejavu

DejaVu Sans bitmap fonts for `php-baremetal/ext-display`. The package ships only pre-baked font headers: no PHP
code and no C code. The SDK compiles them into the firmware font table when you require the package.

| Name | Size | Bitmap data |
| --- | --- | --- |
| `dejavu-sans-12` | 12 px | about 2.8 KB |
| `dejavu-sans-16` | 16 px | about 4.7 KB |
| `dejavu-sans-24` | 24 px | about 10.1 KB |

Coverage: U+0020 to U+007E and U+00A0 to U+00FF (191 glyphs: ASCII and Latin-1, accents included). Glyphs are
anti-aliased at 2 bits per pixel. The fonts are proportional.

## Install

In a project created with `phpbm init`:

```bash
composer require php-baremetal/font-dejavu
```

## Use

```php
<?php
use Baremetal\Display\Font;

$d->text(10, 20, 'Temperatura 24°C', $d->rgb(255, 255, 255), font: Font::get('dejavu-sans-16'));
```

Fonts you do not use still take flash, so require the package only when you need it. The built-in `default`
font stays available.

## Regenerate

The headers are made from DejaVu Sans 2.37 (`ttf/DejaVuSans.ttf` in the `dejavu-fonts-ttf-2.37` archive) with the
`phpbm` baker. The source font is not part of the package.

```bash
for n in 12 16 24; do
  phpbm font:bake DejaVuSans.ttf --name=dejavu-sans-$n --size=$n --bpp=2 --range=0x20-0x7E,0xA0-0xFF --out=fonts
done
```

## License

The fonts are under the Bitstream Vera and DejaVu license, see [LICENSE](LICENSE).
