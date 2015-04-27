Production/README

This directory is a convenient place from which to run the actual
production of the game.  Editing and latex'ing the files here is a
straightforward way to print elements for production, compendium, or
runtime.  For example:

  \documentclass[listblue]{game}
  \begin{document}
  \cJamesBond{}
  \cWarlock{}
  \bAnarchists{}
  \end{document}

will produce all of James Bond's and Warlock's bluesheets followed by
an unowned copy of the Anarchists bluesheet.

The \production command is defined for each type of file to do
something appropriate for production.  Similarly, \compendium is
defined to do something appropriate for printing a compendium.
Therefore

  \documentclass[listblue]{game}
  \begin{document}
  \production
  \end{document}

will produce all the bluesheets for each owner, sorted by owner.
Replacing \production with \compendium will produce one of every
bluesheet.  \compendium usually produces "one of everything" for the
given type, but this may produce odd results based on how things are
set up in Lists/.

Production can be further tweaked using \punt and \unpunt (see
Extras/README-punt).

You can also set up a temporary file wherein you just change the file
option ("listblue," "abil," etc.) and occasionally the contents,
rather than edit the pre-existing files in Production/.  Also,
Extras/gametex.pl (see Extras/README) can be used as a shortcut for
some basic things.

The carditems option produces all normal item cards to be printed on
cardstock.  The paperitems option produces all items that are
ItemEnvelope and ItemPacket macros, to be printed on normal-weight
paper.  The items option produces both of these sets mixed together.
Even if your game is not using cardstock for items, this separation
may still be useful: paperitems will always require further production
(either folding and stapling the packets or stuffing and sealing the
envelopes), while carditems, unless they are or are owned by
subowners, can be distributed as-is.



Workflow: When printing your game, you'll generally use the
latex/dvips/lpr workflow.  You latex a file with:

  latex filename.tex

Then you produce the postscript file based on the resulting .dvi with:

  dvips filename.dvi

Finally, you send to the local printer with:

  lpr -l filename.ps

The -l option tells lpr to send the raw postscript file, which will
preserve print-level postscript commands that automate duplex/simplex
printing.  You can also specify a specific printer with -P.

You can use pdflatex, instead, for previewing files while you write,
but it is not recommended for production.  Automated duplex/simplex
printing requires postscript, as do the various map-drawing commands.



Printing and Collating: Elements print together by type.  You'll
generally latex and print a single file per type (rather than per
owner).  A given file will print quickly because the elements are
batched into a single document, limiting the number of jobs put in the
printing queue and the number of times the printer will need to spin
down and back up.

You'll be able to collate printed materials by the label printed in
the page header, which reflects the ownership of the printed elements
(whitesheets are an exception: their ownership information is only
printed on a separate piece of paper that separates different owners).
The label will generally include the full ownership path of the
elements.  Things owned together will be grouped together.

Transferable elements will not have ownership printed directly on them
(if they are cards, the label will still be printed in the page
header, but not on the item cards themselves).  Elements owned by
something transferable will display their ownership only up to the
transferable thing: a greensheet owned by an item card will show that
it is owned by the card but not give away whose packet the item card
started in.

For cards, a new page is started whenever the ownership changes.  When
printing and collating, you'll be able to give characters their cards
as whole pages and let the players cut them out (obviously, this
should not apply to mempackets).  Subowners (see Lists/README) will
also get separate pages, making it easy to set them aside for extra
production.

\compactcards, placed in the preamble (between \documentclass and
\begin{document}), specifies that ownership changes will not create
page breaks for the entire file of cards.  This may be useful for
saving paper when you are doing the cutting instead of the players.
For transferable cards, no ownership will be printed anywhere.
\compactcards is likely only useful for namebadges and statcards.



Single and Double-Sided Printing: generally, you print by running
latex to produce a .dvi file and dvips to to print to a postscript
printer (or produce a .ps file you print with lpr).  GameTeX documents
include postscript header files to force postscript printers to print
them as duplex (double-sided) or simplex (single-sided) as
appropriate.  This assumes you are using a postscript printer capable
of printing duplex.  These header files will usually override
command-line arguments and similar, so the files will always print
correctly.  All sheets and nearly all cards print double-sided.

You can use \SingleSiding or \DoubleSiding in the preamble to override
the default siding for a given file (the most recent command will take
precedence).  For example

  \documentclass[listchar]{game}
  \SingleSiding
  \begin{document}
  \production
  \end{document}

will print all the game's character sheets single-sided.  This may be
useful for faster printing (though production files print quickly,
regardless, since the sheets are batched into a single file).



Multiple Runs: You can override \gamerun by defining \GAMERUN before
\documentclass.  For example:

  \def\GAMERUN{2}
  \documentclass[listblue]{game}
  \begin{document}
  \production
  \end{document}

will will produce all the bluesheets for each character for the second
run of the game.



Stand-Alone Files: During runtime or even normal production, you may
want to produce materials while bypassing the ownership structure
provided in Lists/.  For a sheet, you can just latex/print the
individual sheet files directly.  For cards, you can use (see
Lists/README) one-shot macros and regular datatype macros, separated
by the \name command to change owners.  For example, to produce a
number of memory packets for different characters:

  \documentclass[mems]{game}
  \begin{document}

  \name{John Smith}
  \memfold{badge \#1234}{That's your long lost brother!}
  \memfold{badge \#\cJamesBond{\MYnumber}}{That's James Bond!}

  \name{Dick Jones}
  \mTest{}
  \memfold{``Rosebud''}{That name sounds familiar.}
  \memfold{trigger}{text}

  \end{document}

This places the structure (and possibly content) information into the
production file rather than the Lists/ database, but it may be useful
for quick work during runtime.

You can use \multi to print multiple copies of something:

  \documentclass[listblue]{game}
  \begin{document}
  \multi{5}{\bArmy{}}
  \end{document}

will give you five unowned copies of the Army bluesheet.

When printing cards, \pageof will give you a full page of a single
card (however many can fit on one page):

  \documentclass[carditems]{game}
  \begin{document}
  \pageof{\iRedRTI{}}
  \pageof{\iGreenRTI{}}
  \pageof{\iBlueRTI{}}
  \end{document}

will give you a page's worth of red RTIs, a page of green RTIs, and a
page of blue RTIs.
