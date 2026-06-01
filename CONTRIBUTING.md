# Contributing to Awesome XRD → Crystal

**Additions, corrections, and translations are warmly welcomed — 欢迎补充、纠正与翻译！**

This list is a community effort. If you notice a missing paper, a wrong link, an incorrect affiliation, an out-of-date venue, or a duplicate entry, please help us fix it.

---

## How to contribute

There are three easy ways to contribute:

1. **Open an issue** — paste the paper title, arXiv id or GitHub link and (if possible) the section it belongs in. The maintainer will add it.
   <https://github.com/Bin-Cao/awesome-xrd2crystal/issues/new>
2. **Open a Pull Request** — edit `README.md` directly, following the entry format below.
3. **Email the maintainer** — for bulk additions (e.g. a whole research direction we missed). Address listed on the [maintainer's homepage](https://bin-cao.github.io/).

All contributors are credited automatically via the [Contributors](README.md#contributors) section at the bottom of the README (rendered from the GitHub contributor graph by [contrib.rocks](https://contrib.rocks)).

---

## Guidelines

- **Chronology.** Entries within each section are ordered **oldest → newest** by the first public release date — i.e. the arXiv preprint date if available, otherwise the journal publication date.
- **One entry per method/paper.** If a follow-up paper substantially extends a previous method, add it as a **separate dated entry** rather than rewriting the old one.
- **Open-access first.** Prefer arXiv, Nature OA, journal HTML or institutional repository links over paywalled DOIs when both exist; include both when useful.
- **Verify pre-prints.** For arXiv submissions, double-check the arXiv id, author list, and affiliation before submitting.
- **Be neutral and descriptive.** Avoid "first to do X" or superlative claims in TL;DRs. Describe what the method *does* and how it is *evaluated*, not where it ranks historically.
- **Match the section.**
  - Models that **classify** a pattern into a known phase / crystal system / space group → *Phase Identification* or *Crystal System / Space Group / Lattice*.
  - Models that **decompose** a multiphase pattern → *Multi-phase Decomposition & Rietveld*.
  - Models that **generate** atomic coordinates from PXRD → *End-to-End PXRD → Crystal Structure (Generative)*.
  - Real-time / beamline / synthesis-loop methods → *Autonomous / In-situ XRD*.
- **Tools vs. datasets.** Reusable Python packages, simulators and refinement engines go in *Simulation, Refinement, and Utility Tools*; pattern collections used for training/evaluation go in *Datasets & Benchmarks*.

---

## Standard entry format

Every paper entry uses the following six- to eight-field block:

```
### YYYY · ShortName — One-sentence tagline

- **Title:** <full paper title>
- **Authors:** <first author> (<affiliation>), …; senior: <senior author> (<affiliation>)
- **Venue:** <journal vol, pp (year)>; arXiv:<id>
- **Paper:** <https://...>
- **Code:** <https://...>          (omit if none)
- **Data:** <https://...>          (omit if none)
- **TL;DR:** <1–3 sentences, factual and neutral>
```

Notes:

- Use **arXiv id and journal citation together** when both exist.
- Wrap URLs in angle brackets (`<https://...>`) so they render as autolinks.
- Keep the TL;DR to **1–3 sentences** and avoid editorial adjectives ("powerful", "novel", "first", …).
- Include benchmark numbers (e.g., MP-20 match rate, Top-k space-group accuracy) only when they are reported in the paper.

### Utility-tool entries

For the *Simulation, Refinement, and Utility Tools* section, use a one-line bullet:

```
- **<ToolName>** — <one-line description>. <https://link-to-docs-or-repo>
```

---

## Link hygiene

- Prefer the canonical journal HTML page over the PDF when both exist.
- For preprints under journal review, list **both** the arXiv link and the (eventual) journal link.
- For code, link the **primary repository** the authors maintain. If an archived snapshot exists (Zenodo, Code Ocean), append it after a `·`.
- When a maintainer rehosts a project (e.g. a fork), prefer the original upstream unless the original is dead.

If you find a broken link, please open an issue with the URL and the section it lives in — fixes welcome as PRs.

---

## Scope

This list is focused on **(P)XRD → crystal structure** machine learning. Out of scope:

- Pure crystal generative models with **no XRD conditioning** (CDVAE, DiffCSP, MatterGen, CrystaLLM, …). They are referenced inside individual entries as base models when relevant, but are not listed standalone here.
- Single-crystal diffraction / electron diffraction work, unless the method also targets powder patterns.
- General property-prediction models (CGCNN, MEGNet, …) that do not consume diffraction data.

If you are unsure whether a paper fits, open an issue and we will discuss.

---

## Licence

By contributing, you agree that your additions are released under the same licence as this repository ([MIT](LICENSE)).
