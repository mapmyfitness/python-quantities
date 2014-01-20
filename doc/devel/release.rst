********
Releases
********

Before creating a release, the version number needs to be updated in
`quantities/__init__.py`. Then Quantities needs to be installed either with::

  python setup.py install

or::

  python setup.py develop

in order proceed with building the release, so the package version numbers will
be advertised correctly for the installers and the documentation.


Creating Source Releases
========================

Quantities is distributed as a source release for Linux and OS-X. To create a
source release, just do::

  python setup.py register
  python setup.py sdist --formats=zip,gztar upload --sign

This will create the tgz source file and upload it to the Python Package Index.
Uploading to PyPi requires a .pypirc file in your home directory, something
like::

  [server-login]
  username: <username>
  password: <password>

You can create a source distribution without uploading by doing::

  python setup.py sdist

This creates a source distribution in the `dist/` directory.


Creating Windows Installers
===========================

We distribute binary installers for the windows platform. In order to build the
windows installer, open a DOS window, cd into the quantities source directory
and run::

  python setup.py build
  python setup.py bdist_wininst

This creates the executable windows installer in the `dist/` directory.


Building Quantities documentation
=================================

When publishing a new release, the Quantities doumentation needs to be generated
and published as well. Sphinx_, LaTeX_ (preferably `TeX-Live`_), and dvipng_ are
required to build the documentation. Once these are installed, do::

  cd doc
  make html

which will produce the html output and save it in build/sphinx/html. Then run::

  make latex
  cd build/latex
  make all-pdf
  cp Quantities.pdf ../html

which will generate a pdf file in the latex directory. Finally, upload the html
content to the http://packages.python.org/quantities/ webserver. To do so::

  cd build/html
  zip -r quantities *

and then visit `the Quantities project page
<http://pypi.python.org/pypi?%3Aaction=pkg_edit&name=quantities>`_ at the Python Package Index to
upload the zip archive.

.. _Sphinx: http://sphinx.pocoo.org/
.. _LaTeX: http://www.latex-project.org/
.. _`TeX-Live`: http://www.tug.org/texlive/
.. _dvipng: http://savannah.nongnu.org/projects/dvipng/
