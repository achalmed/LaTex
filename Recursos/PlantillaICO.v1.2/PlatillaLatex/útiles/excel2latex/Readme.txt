﻿Excel2LaTeX
===========
v3.3

It's difficult to create tables in LaTeX, especially if some columns are calculated. 
Excel2LaTeX allows you to transform the current selection from Excel to LaTeX.

Text formatting (bold, italic), alignment (left, right, centered), and rotation of cell
contents is retained.  Cells spanning multiple columns and/or rows are supported.  
Border lines can be retained at the level of individual cells, or replaced with the 
style of formatting recommended by the booktabs package.  The generated LaTeX 
code can also be placed in a floating table environment.

The LaTeX code can be copied to the clipboard or saved as a LaTeX file, which
then can be included in an existing LaTeX document using the \input command.
You can also specify which ranges of your Excel workbook you want to convert
into LaTeX, and convert them all at once as individual .tex files.

This Excel add-in works best in Microsoft Office 2000 and later (on Windows).
It also works in Office:mac (on Mac OS X), but see the "Known issues" section.


SOURCE
~~~~~~
The development repository and the bug tracker for this package is hosted at
https://launchpad.net/excel2latex .


INSTALLATION
~~~~~~~~~~~~
Just open the file Excel2LaTeX.xla in Excel.  Then you will have two additional 
menu items in your "Tools" menu and a new toolbar with two buttons on it.  For 
Excel 2007 and later, you will have two new buttons in the "Add-Ins" ribbon.  If 
you plan to use the program frequently, you can save it in your addin directory 
and add it with Tools/Add-in.  This way it will be loaded whenever Excel is 
opened.


USAGE
~~~~~
Just select the table to convert and hit the button "Convert table to LaTeX".  You 
will be given the option to save the result to a .tex file, or send it to the clipboard 
(so you can paste it into your LaTeX editor).  Hit the "Store" button to store the 
current settings so you can "Load" them later or "Export all" to LaTeX.


ANNOTATIONS
~~~~~~~~~~~
* Bold and italic are recognized as long as whole cell is in bold or italic.
* Alignment formats (right, left, center) will be recognized for individual cells.
* Cell border lines will be recognized for individual cells (with certain restrictions).
* Font sizes are not supported, because they are handled completely different in
  TeX.
* Cells spanning multiple columns and/or rows are supported.  For this you have to 
  merge the cells in Excel using the format/cells menu and selecting the alignment
  tab.
* The characters %, &, and # are automatically replaced by LaTeX macros
  (e.g. \%), while \, $, _, and ^ can optionally be replaced.
* You can put additional LaTeX formatting commands in the Excel cells, so you 
  don't have to edit the output, if you want some special chars or formats.
* The default file name for export is the name of the selected range (if it has
  one), otherwise it will be the name of the active Excel worksheet.
* Stored tables: It is possible to store the Excel ranges that you want to convert 
  into LaTeX, together with one set of options per range, in the 
  workbook.  Internally, the "list of stored tables" is kept on a hidden worksheet 
  named "Excel2LaTeX", and hence is saved whenever you save your 
  workbook.  The table ranges corresponding to the stored tables are recorded as 
  relative references in the hidden worksheet "Excel2LaTeX"; extensions, 
  contractions or movements of a "stored table" will be reflected 
  automatically.  
  A list view containing the stored tables is shown on the right side of the main 
  form.  A double click on an item in the list of stored tables loads this table; 
  alternatively, you can select the item and hit "Load".  The buttons "Store" and 
  "Overwrite" allow inserting a new or overwriting an existing stored table.  The 
  "Delete" button deletes a selected stored table without prompt.  The 
  "Export all" button converts all selected ranges to LaTeX and writes one .tex 
  file -- don't forget to configure file names properly!  In addition, the new 
  toolbar button and menu item "Convert all stored tables to LaTeX" call the 
  macro LaTeXAllToFiles that also triggers this process.


COPYRIGHT
~~~~~~~~~
Copyright 1996, 1997, 1998, 2001, 2008, 2010, 2011, 2012 by Kirill Müller, 
Andrew Hawryluk, and Joachim Marder.

This work may be distributed and/or modified under the conditions of the LaTeX 
Project Public License, either version 1.3 of this license or (at your option) any 
later version.  The latest version of this license is in 
http://www.latex-project.org/lppl.txt
and version 1.3 or later is part of all distributions of LaTeX version 2005/12/01 
or later.

This work has the LPPL maintenance status `maintained'.
The Current Maintainer of this work is Kirill Müller.
This work consists of the file Excel2LaTeX.xla.


KNOWN ISSUES
~~~~~~~~~~~~
Office Mac: "Copy to clipboard" appends extra null (\0) characters.
Office Mac: Performance is worse than in Windows, converting large ranges might
take minutes or hours.
Office Mac: The functionality is accessible only through the "Format" menu.
Office Mac: The dialog is modal (Windows: modeless).
All: Color not (yet) supported.


BUGS
~~~~
Please report bugs via the bug tracker at https://launchpad.net/excel2latex .


CHANGES
~~~~~~~
Version 3.3: Released on 27 Sep 2012
* Bug fix: Doesn't crash when trying to start conversion when an entire line is
  selected.
* Bug fix: Better conversion of backslashes: '\textbackslash{}' instead of
  '\textbackslash '
* Performance: Improvements by avoiding unnecessary calls to Excel objects

Version 3.2: Released on 26 Mar 2012
* Bug fix: Finally restored compatibility with Office Mac
* Bug fix: Do not add extra alignment tab after \multicolumn{}{}

Version 3.1: Released on 19 May 2011
* If the column width is set to 0, each cell occupies a separate line in the output file
* In booktabs mode, no vertical space is inserted before the top row anymore
* Bug fix: Restored compatibility with Office 2000 and Office Mac
* Bug fix: Form is protected against erroneous entries

Version 3.0: Released on 17 Nov 2010
* CAVEAT: The toolbar buttons and menu items from previous versions of 
  Excel2LaTeX are not deleted automatically.

* CAVEAT: Depending on the formatting of your table, you might require the 
  following packages not required before:
  - bigstrut
  - rotating
  - multirow

* Stored tables: See annotations above.

* More cell formatting options are used in the converted table.
  - Cells with rotated contents are supported.  Requires the "rotating" package.
  - Multirow and multirow-multicolumn cells are supported.  Requires the "multirow" 
    package.
  - A cell formatted as bold and containing inline math formulae is typeset in bold 
    using \boldmath and \unboldmath.
    
* More precise typesetting of cell borders in non-booktabs mode.
    - A column is assumed to have a vertical border if there is a border in any row 
      of this column.  Cells with a vertical border different from the default or 
      without vertical border are typeset using the \multicol command, specifying 
      the border type for this cell.  If both single and double lines are present in 
      one column, a double line is assumed as default for this column.
    - Horizontal rules are typeset using \cline if they do not go straight through 
      from left to right.  Double horizontal lines are converted to single lines in 
      this case.
    - \bigstrut commands are inserted where appropriate.  The number of struts 
      required for a multirow cell is computed correctly.  Requires the "bigstrut" 
      package.

* Bug fix: The type of the left border of a multicolumn cell is determined correctly 
  (in non-booktabs mode).

* Improved file name handling.
  - The target .tex file will be stored in the directory of the Excel worksheet by 
    default.
  - If the target .tex file resides in the directory of the worksheet or in a 
    subdirectory, a relative path to the file is stored.

* The main form is now modeless.  The worksheet can be edited while the form is 
  open.
  - Changes to the contents of the selection are tracked, the LaTeX table in the 
    text box is updated automatically. Changes to cell formatting (font style, 
    borders) are not tracked.
  - The current selection can be set as source range for the current conversion to 
    LaTeX by hitting the large button at the top of the dialog.

* The main form shows up always, even if no range or a multi-area range is 
  selected.

Version 2.3: Released on 16 Nov 2010
* Bug fix: In Office 2007, no error is raised after opening a document anymore.
* Bug fix: When writing the TeX file, no additional newline is appended. 
  Spurious spaces may produce unwanted results.

Version 2.2: Released on 29 Sep 2010
* Save and load settings to/from registry.
* Bug fix: do not add two command buttons to the ribbons in Excel 2007 and 
  later.
* Bug fix: use \textbf and \textit instead of \bf and \it.
* Bug fix: do not use vertical borders for multicolumn environment for 
  booktabs tables.
* Bug fix: correctly determine LaTeX column borders if Excel cell borders 
  are set only for the top and/or left border.
* Internal: avoid copying the range to a hidden worksheet before converting 
  it to LaTeX.
* Internal: various code refactorings.
  
Version 2.1: Released on 18 Sep 2008
* Better character replacement: the previous version only replaced the first
  occurrence of $ or % in a cell.
* Optionally generate a table environment, format the table in the style of the
  'booktabs' LaTeX package, and/or add extra leading indent spaces.
* Better interactivtiy (no refresh button required).
* Bug fix: the previous version would damage formulas that referred to cells
  outside the selection.
  
Version 2.0: Released on 21 Jul 2001
This version is based on modifications by Germán Riaño
* Graphical user interface
* The LaTeX code can be copied to clipboard and then pasted into you editor.
* Better handling of multicolum cells
* doublelines on top border are now handled

Version 1.2: Published on 22 Nov 1998
* The characters % and $ are now converted to the correspondig LaTeX makros

Version 1.1: Published on 12 Apr 1997
* Some small changes to make it run with Excel 97 too

Version 1.0: First published version, Oct 22 1996


OLD RELEASES
~~~~~~~~~~~~
To access older releases of this add-on, please visit
https://code.launchpad.net/excel2latex . Releses of version 2.2 and later
can be downloaded directly from URLs like
http://bazaar.launchpad.net/~mail-kirill-mueller/excel2latex/2.2/files
(susbtitute 2.2 for the version number).
