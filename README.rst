Old ada-mode.el
===============

This is a fork of the old version of ``ada-mode.el`` that was
distributed with Emacs.

I was unable to get the newer packaged version of ``ada-mode.el``,
which uses an external program for indentation, fontification, and
navigation, to work after trying on several operating systems.

However, the old version worked fine for me.

So I dug it out of the `Emacs git repository`_ at `savannah.gnu.org`_.
Basically, I cloned the git repository and then figured out what
commit it was deleted in by doing::

  $ git rev-list HEAD -n 1 -- lisp/progmodes/ada-mode.el
  a13c64204c8ead966789abf8efe176e4f2d4f599

Then I checked out the files involved::

  $ git checkout a13c64204c8ead966789abf8efe176e4f2d4f599^ lisp/progmodes/ada-mode.el lisp/progmodes/ada-prj.el lisp/progmodes/ada-stmt.el lisp/progmodes/ada-xref.el doc/misc/ada-mode.texi doc/docstyle.texi doc/doclicense.texi

The ``^`` at the end of the commit hash says to get the previous
commit.

This formed the initial checking for this repository.

It turns out that Emacs 28 doesn't automatically add ada files to
``auto-mode-alist`` (see `issue #2`_).  So, do the following:

.. _issue #2: https://github.com/tkurtbond/old-ada-mode/issues/2

.. code:: emacs-lisp

   (cl-loop for ext in '("\\.gpr$" "\\.ada$" "\\.ads$" "\\.adb$")
              do (add-to-list 'auto-mode-alist (cons ext 'ada-mode)))


