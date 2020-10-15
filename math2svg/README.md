# math2svg


## Description

This [Lua filter](https://pandoc.org/lua-filters.html)
for [Pandoc](https://pandoc.org/)
converts [LaTeX math](https://en.wikibooks.org/wiki/LaTeX/Mathematics)
to [MathJax](https://www.mathjax.org/) generated
[scalable vector graphics (SVG)](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics)
in any of the [available MathJax fonts](https://docs.mathjax.org/en/latest/output/fonts.html).

This is useful when a CSS paged media engine (such as [Prince XML](https://www.princexml.com))
cannot process complex JavaScript as required by MathJax.
See: <https://www.print-css.rocks> for information about CSS paged media,
a [W3C standard](https://www.w3.org/TR/css-page-3/).

No Internet connection is required for SVG conversions, resulting in absolute privacy.


## Requirements

First, use the package manager of your operating system to install
`pandoc`, `nodejs` and `npm`. `brew` and `choco` are recommended package mangers for
respectively macOS and Windows. See: <https://pandoc.org/installing.html>

```bash
$ sudo apt install pandoc nodejs npm
$ sudo dnf install pandoc nodejs npm
$ sudo yum install pandoc nodejs npm
$ brew install pandoc nodejs npm
> choco install pandoc nodejs npm
```

Then, by means of node's package manager `npm`, install the `mathjax-node-cli` package.
This package comes with the `tex2svg` executable.
Leave out the `sudo` on Windows.

```bash
$ sudo npm install --global mathjax-node-cli
> npm install --global mathjax-node-cli
```


## Usage

To be used as a [Pandoc Lua filter](https://pandoc.org/lua-filters.html).
[MathML](https://en.wikipedia.org/wiki/MathML) should be set as a fallback with the `--mathml` argument.

```bash
pandoc --mathml --filter='math2svg.lua'
```

The math2svg filter is entirely configurable over [`--metadata` key value pairs](https://pandoc.org/MANUAL.html#reader-options).
Nine configuration keys are available with sensible default values.
Hence, depending on your system and intentions, not all keys are necessarily required.

|key|default value|
|:--|:-----------:|
|`math2svg_path`|`'/usr/local/bin/tex2svg'`|
|`math2svg_display2svg`|`true`|
|`math2svg_inline2svg`|`false`|
|`math2svg_speech`|`false`|
|`math2svg_linebreaks`|`true`|
|`math2svg_font`|`'TeX'`|
|`math2svg_ex`|`6`|
|`math2svg_width`|`100`|
|`math2svg_extensions`|`''`|


### Key value `math2svg_path`
This string key value is required when, on your system, the full path to the `tex2svg` executable
of the `mathjax-node-cli` package differs from the default `'/usr/local/bin/tex2svg'`
This is certainly the case on Windows systems.

The full path to `tex2svg` can be found with the following command on \*nix, respectively Windows:

```bash
$ which -a tex2svg
> where tex2svg
```

### Key values `math2svg_display2svg` and `math2svg_inline2svg`
These boolean key values specify whether display math, respectively inline math,
should be converted to SVG by the filter.
The defaults convert display math to SVG, whereas inline math falls back to MathML
when `--mathml` was specified at `pandoc` evocation.
These defaults offer the following benefits:

- MathML output gets generated much faster than SVG output.
- Moreover, MathML is well suited for InlineMath as line heights are kept small.


### Key value `math2svg_speech`
This boolean key value controls whether textual annotations for speech generation are added to SVG formula.
The default is `false`.

### Key value `math2svg_linebreaks`
This boolean key value automatic switches automatic line breaking.
The default is `true`.


### Key value `math2svg_font`
This string key value allows to specify a [MathJax font](https://docs.mathjax.org/en/latest/output/fonts.html) different from the default `'TeX'` font.
The string should correspond to the local directory name of the font in the `mathjax-node-cli` installation directory.
For example, the key value string for the font in `/usr/local/lib/node_modules/mathjax-node-cli/node_modules/mathjax/fonts/HTML-CSS/Gyre-Pagella/` would be
`Gyre-Pagella`.


### Key value `math2svg_ex`
This positive integer key value sets the `ex` unit in pixels.
The default value is `6` pixels.


### Key value `math2svg_width`
This positive integer key value sets the container width in `ex` units for line breaking and tags.
The default value is `100` ex.


### Key value `math2svg_extensions`
This string key value allows to load one or more comma separated [MathJax extensions for TeX and LaTeX](https://docs.mathjax.org/en/latest/input/tex/extensions.html) present on the system.
These MathJaX extensions reside in a subdirectory of the `mathjax-node-cli` installation directory.

Take, for example, the installation directory of the extensions is `/usr/local/lib/node_modules/mathjax-node-cli/node_modules/mathjax/unpacked/extensions/`
It contains a subdirectory `TeX` with the extension file `AMSmath.js`.
This MathJaX extension can be loaded by specifying the string `'TeX/AMSmath'` as the value of the `math2svg_extensions` key.


## Privacy

No Internet connection is established when creating MathJax SVG code using
the `tex2svg` command of [`mathjax-node-cli`](https://github.com/mathjax/mathjax-node-cli).
Hence, formulas in SVG can be created offline and will remain private.
For code auditing, see also:

- <https://github.com/mathjax/MathJax-node>
- <https://github.com/pkra/mathjax-node-sre>
- <https://github.com/mathjax/mathjax-node-cli>


## License

Copyright (c) 2020 Serge Y. Stroobandt

MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


## Contact

```bash
$ echo c2VyZ2VAc3Ryb29iYW5kdC5jb20K |base64 -d
```
