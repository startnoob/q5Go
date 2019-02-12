## q5Go 0.5

This is a tool for Go players which performs the following functions:
- SGF editor
- Analysis frontend for Leela Zero (or compatible engines)
- GTP interface
- IGS client

The basic goal for this program is to provide an everyday SGF editor
that is fast, easy and convenient to use and does everything you could
want out of such a tool.  Some of the more unusual features include a
Go diagram exporting function for sites like lifein19x19.com or
Sensei's library, as well as SVG vector graphics export.  q5go also supports
some non-standard Go variants.

This program is based on the old Qt3 version of qGo, but ported to Qt5
and modernized.

![screenshot](screens/screenshot.png)

Version 0.5 adds the following features:
 * Support for diagrams.  These can be used to either subdivide a game into
   printable diagrams, or to provide a variation display when browsing a
   file in the editor.  The latter case is used by the engine analysis
   mode.
 * A new batch review mode, where the user can choose files to be reviewed
   and hand them off to an engine.  The files can be viewed while the
   analysis is in progress, and there is a winrate graph.
 * A redesigned layout for the user interface.  The various elements of
   the board window (comments, diagram display, game tree, evaluation
   graph and observer list) now exist in docks and can be freely moved
   around.  It is possible to save and restore these layouts.
 * Most icons have been replaced with larger ones, and q5go now uses a
   Qt feature for better results on high-DPI displays.  This is untested,
   I would appreciate feedback as to how well it works on such devices.
 * The command line options have changed.  They are now processed by
   standard library functions and follow normal conventions as a result.

See VERSION_HISTORY for a history of changes.

## Overview of features

### Analysis mode
q5Go supports not only play against AI engines, but can also connect to
Leela Zero to use it as an an analysis tool, displaying statistics such
as win-rates and visit counts, and displaying variations.  This is
available both for local SGF editing, and for observing on-line games.
By middle-clicking or shift-clicking on a displayed variation, it can
be added to the game record.

![screenshot](screens/analysis.png)

There is also a batch analysis mode, where the use can queue a number of
SGF files for analysis. Evaluations and variations are added automatically,
the variations are presented as diagrams.  The file can be observed
during analysis

![screenshot](screens/batch.png)
![screenshot](screens/new-analysis.png)

### Export
q5Go allows the user to export board positions as ASCII diagrams suitable
for Sensei's Library or the lifein19x19.com forums, or in the SVG vector
graphics format which should be suitable for printing.  In both cases,
the user can select a sub-area of the board to be shown in the export,
and it is possible to set a position as the start of move numbering, so
that sequences of moves can be shown in the exported diagram.

![screenshot](screens/export.png)

### SGF diagrams

It is possible to set a game position as the start of a diagram.  This is
has several use cases:
- Subdividing a game record into printable diagrams.  Figures can be
  exported to ASCII and SVG, in whole or in part, just like regular
  board positions.
- Allowing variations to be shown in a separate board display
- Neatly organizing engine lines when performing an analysis

### Configurable appearance

The look of the board and stones can be configured to suit the user's
personal taste.  The stones are generated in a shaded 3D look, and both
the shape and the lighting can be changed.

![screenshot](screens/gostones.jpg)

There are several presets for the wood image, and the user can also
supply a custom file.

![screenshot](screens/gostones2.jpg)

### Configurable user interface layout

All optional elements of the board window reside in freely moveable and
resizable docks, giving the user flexibility to create exactly the layout
they want.  These layouts can be saved and restored, and the program
tries to restore the correct layout whenever a new window is opened.

![screenshot](screens/docks.png)

### Go variants

q5go supports rectangular and toroidal boards.  Note that the latter
can only be saved in a non-standard SGF format since the specification
does not allow for it.  When playing on a torus, q5go can be configured
to extend the board past its regular dimensions, duplicating parts of
the position for a better overview.  Also, the board can be dragged
with the middle mouse button.

![screenshot](screens/variants.jpg)

The screenshot shows the variant game dialog and a (different) position
with both axes set to be toroidal.

## Compiling

On Linux, make a build subdirectory, enter it, and run
```sh
  qmake ../src/q5go.pro PREFIX=/where/you/want/to/install
```
followed by make and make install.  If the pandoc tool is installed, this
README.md file will be converted to html and installed, and can then be
viewed through a menu option.

On Windows, download the Qt tools and import the q5go.pro project file
into Qt Creator.
