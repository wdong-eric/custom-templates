# ED Beamer style

`edbeamer.sty` extracts the reusable setup from `scales-talk.tex` and
`CIAE_EDtweak2.sty`. Copy it beside a new talk and load it with:

```tex
\documentclass{beamer}
\usepackage{edbeamer}
\addbibresource{refs.bib}

\author[Short author]{Full author}
\title[Short title]{Full title}
\institute{Your institute}
\date{Your date}

\begin{document}
\begin{frame}[plain,noframenumbering]
  \titlepage
\end{frame}
\section{Introduction}
\begin{frame}{First slide}
  \begin{myshadowbox}[colback=green!5]
    Your main message.
  \end{myshadowbox}
\end{frame}
\end{document}
```

The style retains UoM blue (`uom`), smoothbars navigation, rounded blocks,
the single-row author/title/frame-count footer, hidden navigation symbols,
dash/asterisk subitems, numbered captions, and bibliography entries without
icons. Sections do not automatically insert outline slides.

It also supplies serif mathematics, `bm`, `booktabs`, `multirow`, `calligra`,
TikZ, `tcolorbox`, `myshadowbox`, and `myfavoriteat`. Biblatex is loaded with
the talk's Biber/authoryear settings and compact `Author+` citations;
`\citet` and `\citep` are available. Keep `\addbibresource` in the talk.

- Wrap a frame with `\miniframesoff` / `\miniframeson` to exclude its
  navigation dot. This preserves the original tweak's internal Beamer hook.
- Use `\setframeofframes{of}` to replace the footer's `/` separator.
- Use `\appendix` before backup slides. `appendixnumberbeamer` handles the
  totals; the talk's unused manual `\backupbegin` / `\backupend` helpers
  are not carried over.
- Keep metadata, plot paths, draft/lecture filters, note-display choices,
  and optional packages such as `media9` in each talk. Use short author/title
  values that fit on one footer row.

Build the self-contained example with a TeX installation including Biber:

```sh
cd beamer-template
latexmk -pdf edbeamer-example.tex
```

The example generates `edbeamer-example.bib` with an illustrative reference.
The original `CIAE_EDtweak2.sty` remains available for existing talks; do not
load both styles in the same document. `scales-talk.tex` now uses `edbeamer`,
but a complete build still requires its external `refs.bib`, `talkplot/`,
and `../../paperplots/` assets.
