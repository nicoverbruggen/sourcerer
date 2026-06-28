# Sourcerer

**Sourcerer** is a modified font based on [Source Serif 4](https://github.com/adobe-fonts/source-serif), optimized for e-readers.

<kbd><img src="./screenshot.png" width='400px'/></kbd>

The original Source Serif 4 variable font is located in `src` and is available under the same OFL as the end result, which is included in `LICENSE`.

## Downloads

Two versions are generated via the pipeline of the [latest release](../../releases/latest):

- **KF_Sourcerer.zip** — Kobo-optimized TrueType fonts with a legacy kern table and `KF` prefix. Use this if you have a Kobo e-reader, this version contains optimizations made with [Kobo Font Fix](https://github.com/nicoverbruggen/kobo-font-fix).
- **Sourcerer.zip** — The standard, unmodified fonts, as TrueType files. Useful for other e-readers and use on your desktop computer or smartphone.

## Project structure

- `src`: Source Serif 4 variable font TTFs
- `build.py`: The build script to generate Sourcerer
- `LICENSE`: The OFL license
- `COPYRIGHT`: Copyright information, later embedded in font
- `VERSION`: The version number, later embedded in font

After running `build.py`, you should get:

- `out/ttf`: final TTF fonts
- `out/kf`: Kobo-optimized KF variants

## Building

Use the prebuilt `fntbld-oci` container:

```bash
podman run --rm -v "$PWD":/work -w /work \
  ghcr.io/nicoverbruggen/fntbld-oci:latest \
  python3 build.py
```

The build script uses `fontTools`, FontForge, and `ttfautohint` from the container to transform the Source Serif 4 variable fonts into Sourcerer. The pipeline instances Regular, Bold, Italic, and Bold Italic; applies Sourcerer's metrics and outline fixes; exports hinted TTFs; post-processes style flags and the lowercase `e` glyph; and generates Kobo `KF_` variants via [Kobo Font Fix](https://github.com/nicoverbruggen/kobo-font-fix).
