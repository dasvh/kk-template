# Customization

The template keeps rendering and user content separate. The committed files
under `pages/`, `templates/`, `commands.tex`, and `packages.tex` provide the
renderer. User-specific metadata, cards, profile text, and cover artwork belong
under ignored `local/`.

## Metadata

Create `local/metadata.tex` with the same command names as the public example:

```tex
\newcommand{\Title}{Kompetenzprofil}
\newcommand{\Author}{Max Mustermann}
\newcommand{\Class}{TIA-42-A}
\newcommand{\Subject}{Dipl. Informatiker/in HF}
\newcommand{\Organisation}{TEKO Schweizerische Fachschule}
\newcommand{\SubmitDate}{20. September 2026}
```

Avoid addresses, phone numbers, private email addresses, enrollment details,
or other metadata that does not belong in the intended publication.

## Cards

Create `local/cards.tex` with one or more `\createCard` calls. Every ID must
exist in the catalog loaded by `templates.tex`. Keep one strongest competence
field selected per card by setting exactly one of the three competence flags to
`1`.

The `Arbeitsergebnis` should describe a completed and traceable result. The
`Qualität` statement should explain how the result can be observed or measured.
Use fictional content only in public examples and do not anonymize a real
portfolio by changing names alone.

## Profile

Create `local/quality-profile.tex` with the profile body. The helper commands
`\qpField`, `\qpList`, `\qualityProfileArbeitsergebnis`,
`\qualityProfileRef`, and `\qualityProfileBullet` are available. For example:

```tex
\phantomsection
\addcontentsline{toc}{section}{Qualifikationsprofil}
\begin{center}
  {\LARGE\textbf{Qualifikationsprofil}}\\[0.3cm]
  {\large\Subject}
\end{center}

\qpField{B7}
\qpList{
  \qualityProfileArbeitsergebnis{B7.3}
}
```

For a table layout, use the public profile example as a starting point. Card
results must be collected before the profile is rendered, which the main
document handles automatically.

## Cover

Create `local/assets/cover.tex` when a different cover is needed. The file is
input inside a TikZ-capable document and should contain a self-contained
TikZ picture or other authorized artwork. Do not copy a school, employer, or
third-party asset into the repository without permission.

## Catalog Changes

Do not edit the catalog casually. If the authoritative edition changes, update
the catalog entries only after comparing every entry, record the edition and
changes in `docs/catalog-source.md`, and review the reuse terms. Keep the
catalog order in `templates.tex` stable so the picker and card headings remain
predictable.
