# Reload a PDF file or save over an opened PDF file

All of the usual PDF viewers that I've tried (Adobe Reader, PDF-XChange, ...) **lock** a file opened with them. That is, the file cannot be overwritten until it is closed in the PDF viewer.

This is inconvenient for developing scripts that generate a PDF file, because a developer would like to see changes in the source code reflected in the PDF preview.

The easiest way I've found to open a PDF file without locking it, is to use [Atom editor][] with [atom-pdf-view][] plugin. The plugin also *auto-reloads* the file on update.

I now prefer to use [Visual Studio Code][] for editing code but I still keep Atom open when I work on PDF file generators to preview changes to the generated PDF files almost in real time.

As a side note, that plugin is based on Mozilla's [pdf.js][] library, so I suspect other previers based on that library would also not lock the file.

* As of the time of writing, Firefox locks an open PDF file.

[pdf.js]: https://github.com/mozilla/pdf.js
[Atom editor]: https://atom.io/
[atom-pdf-view]: https://github.com/izuzak/atom-pdf-view
[Visual Studio Code]: https://code.visualstudio.com/