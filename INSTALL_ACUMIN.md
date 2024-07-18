How to install Acumin
======================

TL;DR:
1. Install fonts
2. Make mapping and update TeX font map
3. Create a LaTeX `.sty` file to use the font
4. Use the font in your LaTeX documents
5. ***Use LuaLaTeX or XeLaTeX for best results***

Here are general instructions for installing the Acumin font for use with LaTeX. These steps may vary depending on your specific LaTeX distribution and system setup.

1. Obtain the Acumin font files:
   - Acumin is a commercial font by Adobe. You'll need to purchase or license it legally.
   - Once obtained, you should have .otf or .ttf files for the font.

2. Install the font on your system:
   - On macOS: Double-click the font files and use Font Book to install them.
   - On Linux: Copy the font files to `~/.local/share/fonts/` or `/usr/local/share/fonts/`.

3. Update the font cache (Linux only):
   - Run `fc-cache -f -v` in the terminal.

4. Make LaTeX aware of the font:
   - Create a directory for local TeX files if you haven't already:
     `mkdir -p ~/texmf/fonts/opentype/adobe/acumin`
   - Copy the Acumin .otf or .ttf files into this directory.

5. Create a font mapping file:
   - Create a file named `acumin.map` in `~/texmf/fonts/map/dvips/acumin/`.
   - Add lines like this for each font variant:
     `acumin-regular Acumin-Regular "T1Encoding ReEncodeFont" <Acumin-Regular.otf`

6. Update TeX's font map:
   - Run `updmap-sys --enable Map=acumin.map`

7. Create a LaTeX package to use the font:
   - Create a file named `acumin.sty` in `~/texmf/tex/latex/acumin/`.
   - Add the necessary commands to define the font for LaTeX.

This last step will be tricky. See the following example for a basic `acumin.sty` file:

```latex
\NeedsTeXFormat{LaTeX2e}
\ProvidesPackage{acumin}[2024/07/17 Acumin font]

\RequirePackage{fontspec}
\RequirePackage{xunicode}
\RequirePackage{xltxtra}

\newfontfamily\acumin{Acumin}[
  Extension = .otf,
  UprightFont = *-RPro,
  BoldFont = *-BdPro,
  ItalicFont = *-ItPro,
  BoldItalicFont = *-BdItPro,
  SlantedFont = *-RPro,
  BoldSlantedFont = *-BdPro,
  Scale = 1.0,
]

\newcommand{\textacumin}[1]{{\acumin #1}}
% \newcommand{\acumin}{\acumin\selectfont}
```

Note that this process can be complex and may vary depending on your specific LaTeX distribution and system setup. If you encounter issues, you might need to consult your LaTeX distribution's documentation or seek help from a LaTeX forum.
