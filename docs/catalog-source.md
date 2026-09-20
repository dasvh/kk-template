# Catalog Source

The catalog in `templates/` is a structured transcription of the competency
descriptions in the following source:

- Issuer: Staatssekretariat für Bildung, Forschung und Innovation (SBFI)
- Title: `Rahmenlehrplan für Bildungsgänge der höheren Fachschulen «Informatik»`
- Trägerschaft named by the source: Verein Trägerschaft RLP HF Informatik
- Edition/status: Rahmenlehrplan valid from 10 October 2022; the SBFI page marked it current when retrieved
- Approval/publication date: approved by SBFI on 10 October 2022
- Source page: <https://www.becc.admin.ch/becc/public/bvz/beruf/show/321>
- Direct document: <https://www.becc.admin.ch/becc/public/bvz/beruf/download/13123>
- Retrieval date: 2026-09-20

The competency overview is in source pages 10-16. The detailed descriptions
and levels are in source pages 18-29. This repository uses the IDs A1-A3 and
B4-B15 and the competency wording as the catalog labels.

## Modifications

This project does not reproduce the complete Rahmenlehrplan. It extracts the
competency IDs and short descriptions needed by the picker and card renderer.
The source PDF contains line wrapping, hyphenation, OCR-like extraction
artifacts, and occasional differences between the overview and detailed pages.

The committed text:

- normalizes line breaks, hyphenation, whitespace, and typography;
- uses the competency ID as the final parenthetical marker;
- follows the detailed competency wording where the overview is abbreviated;
- keeps the catalog in the A1-A3, B4-B15 order;
- does not include the source document's explanatory paragraphs, reference
  tables, competency levels, or institutional branding.

The catalog is a convenience for authoring and is not an official TEKO or SBFI
catalog.
