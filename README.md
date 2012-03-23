PYLORI: PYthon videoLecture Offline RevIew
==========================================

Pylori comes with a set of command-line tools to enjoy 
[videolectures.net](http://videolectures.net) when disconnected: 

* `pylori_dl` - Lecture downloader that downloads video and slides from 
videolectures.net.
* `pylori` - Lecture player that plays the video and slides downloaded by 
`pylori_dl`.
* `pdf2png` - A tool to convert PDF slides downloaded by `pylori_dl` to 
high resolution images for `pylori`.


Installation
------------

Pylori requires 
[Python](http://www.python.org/),
[wxPython](http://www.wxpython.org/),
[MPlayer](http://www.mplayerhq.hu/),
[ImageMagick](http://www.imagemagick.org/).

On Mac OS X, you could install the above packages through
[MacPorts](http://www.macports.org/) by:

    $ sudo port install python27 py27-wxpython-devel mplayer-devel ImageMagick

On Linux, you could install required packages with the 
package management tool on your system. For example, on Ubuntu:
    
    $ sudo apt-get install python python-wxgtk2.8 mplayer imagemagick


Usage
-----

    pylori_dl [-v] http://videolectures.net/XXX/[video/NNN/]

If the option `-v` or `--skip_video` is specified, pylori_dl will 
download only slides and skip the video.

    pylori DIRECTORY

`DIRECTORY` is the directory created by pylori_dl.

    pdf2png [-d DENSITY] PDF [PAGES [PAGES ...]]

pdf2png will generate PNG images in the current directory from the 
specified PDF slides.
`PDF` is the pdf slides downloaded by pylori_dl.
`PAGES` could be a single page number or a range to page numbers 
in the format of `a-b` without spaces in between. 
For example, `PAGES` could be `1-3` or `3-1` which are equivalent
to `1 2 3` and `3 2 1` respectively. If `PAGES` is omitted, all the pages
of the PDF slides are generated.
`DENSITY` is the density of the images to generate.


Examples
--------

Supposing you are interested in [this lecture]
(http://videolectures.net/nipsworkshops2011_ghahramani_nonparametrics/),
you can run the following to download the materials of that lecture:

    $ pylori_dl http://videolectures.net/nipsworkshops2011_ghahramani_nonparametrics/

When pylori_dl is done, a directory named after the title
of the lecture will be created, in this case, 
"Why Bayesian nonparametrics?". You can then watch the lecture by:

    $ pylori Why\ Bayesian\ nonparametrics\?/

Usually a PDF version of the slides will also be available, which
will be downloaded by pylori_dl and placed in the created directory.
If you are not satisfy with the image quality of the original slides,
you can use pdf2png to generate a copy with higher resolution from
the PDF slides.

    $ cd Why\ Bayesian\ nonparametrics\?/
    $ pdf2png nipsworkshops2011_ghahramani_nonparametrics_01.pdf

After the high resolution images are generated, you have to
edit `sync.txt` in the directory to notify pylori to use these images 
just by substituting the image names ended with `jpg`
with `png` which could be done easily with any text editors.

Pylori can also be used for lectures with multiple sections such as
[this one]
(http://videolectures.net/mlss07_rasmussen_bigp/).
In this example, if you want to download, say the fourth part, you can specify
the URL in the following format:

    $ pylori_dl http://videolectures.net/mlss07_rasmussen_bigp/video/4/

In the multi-part cases, a single section might just involve part of the 
pages in the PDF slides. To generate the slide images for that particular
section, you can specify the corresponding page numbers (or ranges). 
In the same example, it is:

    $ cd Bayesian\ inference\ and\ Gaussian\ processes-4/
    $ pdf2png -d 300 . 38-43 42-44 42 41 44 41 44 43

Without using `-d 300` the generated images will be
not much better than the original ones, so a larger density such as 300
should be specified explicitly. 

