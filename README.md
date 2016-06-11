# HastyScribe

_HastyScribe_ is a simple command-line program able to convert [markdown](http://daringfireball.net/projects/markdown) files into HTML files.

## Usage

**hastyscribe** _filename-or-glob-expression_ **[** _\<options\>_ **]**

Where:

  * _filename-or-glob-expression_ is a valid file or [glob](http://en.wikipedia.org/wiki/Glob_(programming)) expression that will be compiled into HTML.
  * The following options are supported:
    * **\-\-field/&lt;field&gt;=&lt;value&gt;** causes {{hs}} to set a custom field to a specific value.
    * **\-\-notoc** causes {{hs}} to output HTML documents _without_ automatically generating a Table of Contents at the start.
    * **\-\-user-css=&lt;file&gt;** causes {{hs}} inserts the contents of the specified local file as a CSS stylesheet. 
    * **\-\-output-file=&lt;file&gt;** causes {{hs}} to write output to a local file (Use [\-\-output-file=-](class:opt) to output to standard output).
    * **\-\-watermark=&lt;file&gt;** causes {{hs}} to embed and display an image as a watermark throughout the document. 

## FAQs

### Why is _HastyScribe_ different from other markdown converters?

Because:

* It is a cross-platform, self-contained executable file
* It comes with its own stylesheet, which is automatically embedded into every HTML document, along with all the needed web fonts
* It is built on top of [Discount](http://www.pell.portland.or.us/~orc/Code/discount/), which means that besides standard markdown you also get:
  * strikethrough
  * automatic Table of Contents generation
  * [SmartyPants](http://daringfireball.net/projects/smartypants/) substitutions
  * paragraph centering
  * image sizes
  * definition lists
  * alphabetic lists
  * pseudo-protocols to generate `span` tags with arbitrary CSS classes, `abbr` tags, and anchors
  * class blocks
  * tables
  * fenced code blocks
  * [Pandoc](http://johnmacfarlane.net/pandoc/)-style document headers
* It automatically embeds any referenced image via data URI
* It has supports for text snippets

### What can I use it for?

_HastyScribe_ is best suited to produce self-contained documents such as essays, meeting notes, project status documents, and articles.

### What language is _HastyScribe_ implemented in?

HastyScribe is implemented in [Nim][nim], a very expressive language that compiles to C and is able to generate small, standalone and self-contained executable files.

### How do I build _HastyScribe_ from source?

First of all you need a **libmarkdown.a** static library. You can either grab one precompiled (for Windows or Mac OS X) from the [vendor](https://github.com/h3rald/hastyscribe/blob/master/vendor) folder of the HastyScribe repository or build your own. 

If you choose to build your own:

1. Clone the discount [repository](https://github.com/Orc/discount).
2. In the directory containing the Discount source code, run the following commands:

   ```
   ./configure.sh --with-tabstops=2 --with-dl=both --with-id-anchor --with-github-tags --with-fenced-code --enable-all-features

   make
   ```

  Tip: If you are on Windows, you can compile Discount using [MinGW-w64](http://mingw-w64.yaxm.org/doku.php).

Once you have a **libmarkdown.a** static library for your platform:

1. Download and install [Nim][nim].
2. Clone the HastyScribe [repository](https://github.com/h3rald/hastyscribe).
3. Put your **libmarkdown.a** file in the **vendor** directory.
4. Run **nim c hastyscribe.nim**

[nim]: http://nim-lang.org/
