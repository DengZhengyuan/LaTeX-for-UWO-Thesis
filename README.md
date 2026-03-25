# LaTeX Template for a Western University PhD Thesis

This repository provides a PhD thesis template for Western University. It was
adapted from a successfully submitted thesis and then cleaned up for public use.
The template is intended as a practical starting point rather than an official
university release.

The setup follows the thesis-formatting guidance published by the School of
Graduate and Postdoctoral Studies at Western University:
[Western thesis formatting](https://grad.uwo.ca/academics/thesis/formatting.html)

## Toolchain

The template is designed for:

- `pdflatex`
- `biber`
- `makeindex`

The supported build sequence is:

```bash
pdflatex westernthesis.tex
biber westernthesis
makeindex westernthesis.nlo -s nomencl.ist -o westernthesis.nls
pdflatex westernthesis.tex
pdflatex westernthesis.tex
```

This repository is written for a modern local TeX Live / MacTeX installation
and should also remain friendly to later use on Overleaf.

## Project structure

- `westernthesis.tex`: root document, package setup, global formatting, chapter
  list, and appendix list.
- `westernthesis.bib`: bibliography database used throughout the thesis.
- `preliminaries/`: front matter such as the abstract, acknowledgements,
  summary for lay audience, nomenclature, and curriculum vitae.
- `chapters/`: thesis chapters plus appendix files.
- `fig/`: figures used by the sample content.
- `westernthesis.pdf`: example compiled output currently tracked in the
  repository.

## What to edit first

Start with the following files:

- `westernthesis.tex` to enable or disable chapters and appendices.
- `preliminaries/*.tex` for front matter.
- `chapters/*.tex` for the main thesis content.
- `westernthesis.bib` for references.

The template already includes examples of:

- chapter-level bibliographies with `biblatex`
- nomenclature generation with `nomencl`
- figures, tables, equations, and appendix chapters

## Working with chapters and appendices

### Main chapters

Add or remove chapters by editing the `\include{...}` lines in
`westernthesis.tex`.

### Appendices

Appendices are handled with the standard LaTeX `\appendix` mechanism. To add a
new appendix:

1. Duplicate an appendix file in `chapters/`.
2. Rename it, for example `chapters/appendix_2.tex`.
3. Add a matching `\include{chapters/appendix_2}` line below `\appendix` in
   `westernthesis.tex`.

Appendices are listed automatically in the main table of contents. You do not
need to maintain a separate "List of Appendices" by hand.

If you do not need appendices, comment out the `\appendix` line and the
appendix `\include{...}` lines in `westernthesis.tex`.

## Bibliography and nomenclature

Each sample chapter uses its own `refsection`, so chapter references are printed
at the end of that chapter. The curriculum vitae section also has its own
bibliography block.

The nomenclature list is configured in `preliminaries/nomecl.tex`. After
running `pdflatex`, generate the nomenclature with:

```bash
makeindex westernthesis.nlo -s nomencl.ist -o westernthesis.nls
```

## Troubleshooting

- If citations are missing, rerun `biber westernthesis` and then run
  `pdflatex` twice.
- If the nomenclature list is empty, rerun the `makeindex` command shown above.
- If the table of contents, references, or appendix numbering looks stale, do a
  full rebuild instead of a single `pdflatex` pass.
- If you move the project to another environment, make sure `biber` is
  available; some minimal TeX installations do not install it by default.

## Notes

- This template keeps the original `report`-class workflow instead of wrapping
  everything into a custom class file.
- The repository includes sample text and figures only to demonstrate structure.
  Replace them with your own material before submission.
