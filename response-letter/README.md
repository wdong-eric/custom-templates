# Response letter template

Copy `responseletter.sty` and `response_letter.tex` into a new manuscript
directory, then edit the metadata and response text in the `.tex` file.
The example uses `\documentclass[11pt]{article}` and loads the style with
`\usepackage{responseletter}`.

The style preserves the original A4 layout with 20 mm margins, Times-style
text and mathematics (`mathptmx` and `txfonts`), italic referee comments,
blue manuscript quotations, and Aquamarine hyperlinks. T1 font encoding
also makes angle-bracket placeholders render correctly.
It loads `natbib`, `graphicx`, `amsmath`, `bm`, `enumitem` (including inline
lists and short labels), and `subcaption`.

## Writing responses

```latex
\begin{refereecomment}{1}
  Please clarify the assumptions.

  Comments can contain multiple paragraphs, equations, and lists.
\end{refereecomment}

\begin{authorresponse}
  We have clarified the assumptions in Section 2.
  \begin{manuscriptchange}
    We assume that the background is stationary.
  \end{manuscriptchange}
\end{authorresponse}
```

- `refereecomment` takes an explicit label, such as `1` or `2(a)`, and adds
  the trailing period. Match the referee's report; numbering does not advance
  or reset automatically.
- `authorresponse` prints **Authors' response:** before normal response text.
- `manuscriptchange` indents quoted manuscript text and makes the whole block
  blue, including multiple paragraphs and equations. Styling is local to each
  environment.

Use normal `\section*` and `\subsection*` headings for different referees,
editors, or minor comments. Keep `\title`, `\author`, and any `\date` setting
in the document; `\date{}` hides the date.

The original `\todo{...}` and `\figuretag{...}` helpers are also available.
Place `\figuretag{R1}` inside a `figure`, before `\caption`, and put any
`\label` after the caption. This changes that figure's displayed label and
hyperlink target without consuming a normal figure number. Use distinct
tags such as `R1` and `R2` to avoid collisions with ordinary figure numbers.

## Build and references

From the directory containing the two files, run:

```sh
latexmk -pdf -interaction=nonstopmode -halt-on-error response_letter.tex
```

The example compiles without a bibliography or external figures. For
references, add a `response.bib` file, cite entries with `\citet` or `\citep`,
and uncomment the bibliography lines at the end. Copy `aasjournalv7.bst`
from this repository's `custom-journal-template` directory into the new
manuscript directory, or choose another installed `natbib`-compatible style
such as `plainnat`. Bibliography files and style choices belong in the
document, so the `.sty` file has no manuscript-specific paths.
