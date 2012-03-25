PYLORI: PYthon videoLecture Offline RevIew
==========================================

Pylori comes with a set of command-line tools to enjoy
`videolectures.net <http://videolectures.net>`_ when disconnected:

-  **pylori\_dl** - to download video and slides from videolectures.net
-  **pylori** - to play the video and slides downloaded by pylori\_dl
-  **pdf2png** - to convert PDF slides downloaded by pylori\_dl to high
   resolution images for pylori

Installation
------------

Pylori requires 
`Python <http://www.python.org/>`_,
`wxPython <http://www.wxpython.org/>`_,
`MPlayer <http://www.mplayerhq.hu/>`_,
`ImageMagick <http://www.imagemagick.org/>`_.

On Mac OS X, you could install the above packages through
`MacPorts <http://www.macports.org/>`_::

    $ sudo port install python27 py27-wxpython-devel mplayer-devel ImageMagick

On Linux, you could install required packages with package management
tools on your system. For example, on Ubuntu::

    $ sudo apt-get install python python-wxgtk2.8 mplayer imagemagick

Usage
-----

::

    pylori_dl [-v] http://videolectures.net/XXX/[video/NNN/]

pylori\_dl downloads video and all the slides of a lecture specified by
the given URL, and put them in a directory named after the title of the
lecture. If ``-v`` or ``--skip_video`` is specified, pylori\_dl will
download only slides and skip the video.

::

    pylori DIRECTORY

pylori plays the video lecture and shows slides syncing with the video
on a separate window. ``DIRECTORY`` is the directory created by
pylori\_dl that contains lecture materials.

::

    pdf2png [-w WIDTH] [-m] DIRECTORY [PAGES [PAGES ...]]

pdf2png will find PDF slides in ``DIRECTORY``, the directory created by
pylori\_dl, and convert it to high resolution PNG images. The generated
images are put into ``DIRECTORY``.

The option ``PAGES`` specifies page numbers of PDF to be used for the
video in the *exact* order. ``PAGES`` could be a single page number or a
range of page numbers in the format ``a-b`` without spaces in between.
For example, ``1-3`` and ``3-1`` are equivalent to ``1 2 3`` and
``3 2 1`` respectively. If ``PAGES`` is omitted, all pages of PDF are
generated.

``WIDTH`` is the width of outputting images, which defaults to 840.

When ``-m`` or ``--match`` is specified, original low resolution images
are automatically matched with PDF pages. ``PAGES`` are ignored when
this option is used.

pdf2png will also make pylori to display new images afterward.

Examples
--------

Supposing you are interested in 
`this lecture <http://videolectures.net/nipsworkshops2011_ghahramani_nonparametrics/>`_,
you can run the following to download the materials of that lecture::

    $ pylori_dl http://videolectures.net/nipsworkshops2011_ghahramani_nonparametrics/

When pylori\_dl is done, a directory named after the title of the
lecture will be created, in this case, "Why Bayesian nonparametrics?".
You can then watch the lecture by::

    $ pylori Why\ Bayesian\ nonparametrics\?/

When a PDF version of the slides is available, pylori\_dl will download
and place it in the created directory as well. If you are not satisfy
with the quality of the original slides snapshots, you can use pdf2png
to generate a higher resolution copy from PDF slides::

    $ pdf2png Why\ Bayesian\ nonparametrics\?/

pylori can also be used for lectures with multiple sections such as
`this one <http://videolectures.net/mlss07_rasmussen_bigp/>`_. 
In this example, if you want to download, say, the fourth part, you can 
specify the URL like the following format::

    $ pylori_dl http://videolectures.net/mlss07_rasmussen_bigp/video/4/

In the multi-part cases, a single section might just involve part of the
pages in PDF slides. To generate the slide images for that particular
section, you can specify the corresponding page numbers (or ranges)
manually. For the same example, it is::

    $ pdf2png Bayesian\ inference\ and\ Gaussian\ processes-4/ 38-43 42-44 42 41 44 41 44 43

pdf2png also provides an auto matching option ``-m`` to take care of
everything::

    $ pdf2png -m Bayesian\ inference\ and\ Gaussian\ processes-4/

When ``-m`` is used, pdf2png will output the matched page numbers so you
can use them in the future to save time.
