# Kompetenzkarten Template

This repository is an unofficial community template for creating
`Kompetenzkarten` and a linked `Qualifikationsprofil` for the HF Informatik
context. It is not maintained, approved, or endorsed by TEKO. TEKO has no
responsibility for this project or for documents generated with it.

The repository contains reusable LaTeX rendering code, the competency catalog,
and short fictional examples. It intentionally contains no personal portfolio,
employer, customer, project, incident, or infrastructure information.

## Requirements

Install a TeX distribution with:

- XeLaTeX (`xelatex`)
- `latexmk`
- the TeX package containing Fira Sans

Task is optional. The documented commands use only XeLaTeX and `latexmk`; the
included `Taskfile.yml` adds convenient build and clean tasks. The examples are
written for a current TeX Live installation on macOS or Linux.

## Build

Build both documents with:

```sh
task
```

Or without Task:

```sh
mkdir -p build
latexmk -pdfxe -jobname=kompetenzprofil -interaction=nonstopmode -halt-on-error -file-line-error -Werror -outdir=build main.tex
latexmk -pdfxe -jobname=kompetenzkatalog -interaction=nonstopmode -halt-on-error -file-line-error -Werror -outdir=build picker.tex
```

The Task commands write:

- `build/kompetenzprofil.pdf`: title page, qualification profile, and landscape cards;
- `build/kompetenzkatalog.pdf`: all catalog groups and competency IDs.

Generated files are ignored by Git. Building does not open a PDF; use
`task open-cards` or `task open-picker` on macOS when that is useful.

## Personal Files

Keep user-specific content under the ignored `local/` directory:

```text
local/
|-- metadata.tex
|-- quality-profile.tex
|-- cards.tex
`-- assets/
    `-- cover.tex
```

The public examples are used when these files are absent. The main document
automatically uses these local files when they exist:

- `local/metadata.tex` replaces `metadata.example.tex`;
- `local/cards.tex` replaces `pages/03-cards.example.tex`;
- `local/quality-profile.tex` replaces `pages/02-quality-profile.example.tex`;
- `local/assets/cover.tex` replaces the example TikZ cover.

Start by copying the example files into `local/` and then edit them. Do not
commit the directory. `.gitignore` only prevents new local files from being
added; it does not remove information that was already committed to Git.

## Creating Cards

The card API is:

```tex
\createCard{ID}
  {Arbeitsergebnis}
  {Qualität}
  {Umfeld}
  {Fachkompetenz}
  {Methodenkompetenz}
  {Sozialkompetenz}
  {Unterrichtsfach / Grundlagenwissen}
```

`ID` must be an ID from the catalog, such as `A1.7` or `B7.3`. The remaining
arguments are:

1. `Arbeitsergebnis`: a concrete completed result, normally written in German
   perfect tense;
2. `Qualität`: an observable or measurable quality statement;
3. `Umfeld`: a short context that does not disclose confidential information;
4. `Fachkompetenz`: `1` when specialist competence is the strongest field,
   otherwise `0`;
5. `Methodenkompetenz`: `1` when methods or instruments are the strongest
   field, otherwise `0`;
6. `Sozialkompetenz`: `1` when interaction or self-management is the strongest
   field, otherwise `0`;
7. `Unterrichtsfach / Grundlagenwissen`: the supporting school subjects.

Use exactly one strongest competence field per card. The examples are synthetic
and are only an API demonstration, not evidence of completed work.

## Qualification Profile

The main document reads the card file once in collection mode before rendering
the profile. Each `\createCard` stores its `Arbeitsergebnis` under its ID.
`\qualityProfileArbeitsergebnis{A1.7}` then reuses that text and creates a
hyperlink to the corresponding card. A profile can also use
`\qualityProfileBullet[A1.7,A1.8]{A concise summary}` for a manually condensed
entry.

The profile is a selection of card results, not a second source of private
evidence. Review every link and every statement for the current school
requirements before submission.

## Catalog

`templates.tex` is the canonical catalog entry point. It loads the official
groups A1-A3 and B4-B15 in their catalog order. The full source, edition,
retrieval date, normalization choices, and reuse caution are recorded in
`docs/catalog-source.md`.

The catalog is not a substitute for the current official Rahmenlehrplan.
Check the current SBFI source and current school requirements before using an
ID or description in a submission.

## Licensing And Notices

Original template code and documentation are covered by the MIT License. The
catalog descriptions are derived from the public SBFI Rahmenlehrplan and are
not claimed as original work. The source and reuse caution are documented in
`docs/catalog-source.md`; additional notices are in
`THIRD_PARTY_NOTICES.md`.

Users are responsible for checking the current source terms, school rules, and
any permission needed for redistribution. This repository is not an official
TEKO publication.
