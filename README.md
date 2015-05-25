
InfoQube User Manual to CHM Conversion
======================================

[InfoQube][] is an information management system for Windows. The online
[user manual][IQmanual] is a community project.

Back in 2010, a number of users were working on creating an offline version.
As part of that effort, I wrote a Perl script that could be used to help
convert a saved version of the manual, so it could be compiled into
[HTML Help][CHM] (CHM) format.

A big thanks to the great people on the InfoQube community website who helped
make this possible (Pierre, KeithB, Armando, and others).

[InfoQube]: http://www.infoqube.biz/
[IQmanual]: http://www.sqlnotes.net/drupal5/index.php?q=node/48
[CHM]: https://en.wikipedia.org/wiki/Microsoft_Compiled_HTML_Help


Detailed Instructions
---------------------

Make sure you have [Perl][] and the [HTML Help Workshop][hhw] installed.
 
Create a folder, and put the `dump2chm.pl` Perl script into it.
 
Open the printer friendly version of the top level page of the IQ User manual
in Internet Explorer or Chrome:

http://www.sqlnotes.net/drupal5/index.php?q=book/export/html/2043

Wait until the entire page has loaded with all graphics.

In IE, choose File->Save As... and select "Webpage, complete", and "Unicode
(UTF-8)", and save to the folder you put the script in. In Chrome, choose
"Save page as...".
 
Open a command prompt, and run the script with the name of the saved HTML page
as argument:

`dump2chm InfoQube.htm`

This splits the saved HTML file into one file for each node of the manual,
and generates the project files required to compile the CHM.
 
Open `index.hhc` in your favorite text editor, and move the line near the top
that links to `node2043.html` down one line, and change `node2043.html` to
`index.html`, and `value="1"` to `value="11"`. In the current version, this
means changing:

```.html
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML//EN">
<HTML><HEAD></HEAD><BODY>
<OBJECT type="text/site properties">
<param name="FrameName" value="right">
</OBJECT>
<LI><OBJECT type="text/sitemap"><param name="Name" value="InfoQube User Manual (node 2043)"><param name="Local" value="node2043.html"><param name="ImageNumber" value="1"></OBJECT>
<UL>
<LI><OBJECT type="text/sitemap"><param name="Name" value="1. Introduction (node 33)"><param name="Local" value="node33.html"><param name="ImageNumber" value="11"></OBJECT>
```

into:

```.html
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML//EN">
<HTML><HEAD></HEAD><BODY>
<OBJECT type="text/site properties">
<param name="FrameName" value="right">
</OBJECT>
<UL>
<LI><OBJECT type="text/sitemap"><param name="Name" value="InfoQube User Manual"><param name="Local" value="index.html"><param name="ImageNumber" value="11"></OBJECT>
<LI><OBJECT type="text/sitemap"><param name="Name" value="1. Introduction (node 33)"><param name="Local" value="node33.html"><param name="ImageNumber" value="11"></OBJECT>
```

Now run the HTML Help compiler on the project file:

`hhc index.hhp`

And you should have a shiny new `InfoQube.chm`.

[Perl]: http://www.perl.org/
[hhw]: http://go.microsoft.com/fwlink/?LinkId=14188


License
-------

This projected is licensed under the terms of the [MIT license](LICENSE).

Please note that this covers only the script, the contents of the generated
files are licensed under their original license.
