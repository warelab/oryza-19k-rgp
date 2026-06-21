---
title: GrameneOryza
---

**Review.** An integrated gene search interface, Ensembl-based genome browser, and FTP site serving the 19K-RGP across all five references — with the stable Ensembl REST API for gene, region, variant-effect, and sequence queries.

[Open GrameneOryza ↗](/gramene)

## README — what it is & what it hosts

The FTP holds the per-reference variant calls and their predicted effects; the browser visualizes them on the location, gene, and variation pages. Because GrameneOryza is built on Ensembl, the **Ensembl REST API** (`rest.ensembl.org`) gives documented, stable access for *Oryza sativa* — see the [Ensembl REST reference](/api).

> **Use this when…** you need gene models, the predicted consequence of a variant (VEP), cross-reference coordinates, or to stream a VCF slice via a track hub / [remote tabix](/api).

## Tutorial — the genome browser (OsMADS50)

1. From the *location* page, search `OsMADS50` to reach its *gene* page.
2. Open the *variation* page and enable the 19K-RGP variation track.
3. Click a variant to inspect its predicted effect.

A video walkthrough is available at [oryza.gramene.org/videotutorials](https://oryza.gramene.org/videotutorials).

## Workflow — a locus' variants & effects via REST (no download)

Goal: for *MADS14* (`Os03g0752800`), pull the gene model, all overlapping variants, and their predicted consequences. `lookup/id` → `overlap/region` (feature=variation) → `vep` → a tidy variant×consequence table. See [Workflow A](/workflows); the runnable notebook is on [Resources](/resources).

## Examples

**curl**

```bash
# Gene -> coordinates
curl -s "https://rest.ensembl.org/lookup/id/Os03g0752800?content-type=application/json"
# Variants overlapping the locus
curl -s "https://rest.ensembl.org/overlap/region/oryza_sativa/3:31031753-31041563?feature=variation;content-type=application/json"
# Predicted consequence (region/<chrom>:<start>-<end>/<alt>)
curl -s "https://rest.ensembl.org/vep/oryza_sativa/region/3:31037240-31037240/A?content-type=application/json"
```

**Python**

```python
import oryza19k as o19
gene = o19.lookup_gene("Os03g0752800")                       # MADS14
vars = o19.region_features("3:31031753-31041563", feature="variation")
vep  = o19.vep_effects("3:31037240:A")                       # -> intron_variant
```

## Access & cite

The [Ensembl REST API](/api) (`rest.ensembl.org`) is **public and stable now**, no login. **Review** applies only to the browser/FTP during peer review: the 19K-RGP rice resources are now live at [oryza19k.gramene.org](https://oryza19k.gramene.org) (reviewer credentials provided to the editor), moving to public, login-free production endpoints at publication. The durable variant archive is the [European Variation Archive (PRJEB105137)](https://www.ebi.ac.uk/eva/?eva-study=PRJEB105137), also documented under [Archives](/platforms).

Cite: Tello-Ruiz *et al.* (Gramene, *NAR*); the GrameneOryza database paper; the Ensembl REST API.
