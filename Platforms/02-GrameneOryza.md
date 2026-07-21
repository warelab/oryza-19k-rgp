---
title: Gramene Oryza
---

An integrated gene search interface, Ensembl-based genome browser, and FTP site serving the 19K-RGP across all five references.

[Open Gramene Oryza ↗](/gramene)


## README — what it is & what it hosts

This Gramene *Oryza* instance is dedicated to the 19K-RGP data set. The 19K-RGP genotypes were mapped against all five platinum references, one per major *Oryza sativa* subpopulation:

| Reference | Subpopulation | Assembly |
| --- | --- | --- |
| Nipponbare | Japonica (GJ) | IRGSP-1.0 |
| IR64 | indica (XI) | IR64RS2 |
| Minghui 63 | indica (XI) | MH63RS3 |
| N22 | aus | *to confirm* |
| ARC 10497 | aromatic (Basmati) | *to confirm* |

For each reference, Gramene Oryza serves the genome assembly, gene models and annotation, and the 19K-RGP variation data (SNPs + InDels with predicted effects).

- An integrated **[gene search interface](/gramene)** includes rapid access to accessions from the 19K-RGP with predicted loss-of-function alleles in its Germplasm tab, with links to IRRI for obtaining seeds.
- The **[Ensembl genome browser](http://oryza-ensembl-dev.gramene.org/index.html)** visualizes variant data on the location, gene, and variation pages and integrates missense variation within Alphafold predicted protein structures.
- Bulk access to variant calls and their predicted effects are provided via the **[FTP site](https://ftp.gramene.org/oryza/19K-RGP/)**.
- Programmatic access to Gramene data is offered through two services: the **[Ensembl REST API](https://data.gramene.org/pansite-ensembl-108)** and the **[Gramene search API](https://data.gramene.org/oryza_v9)**.


## Tutorial

1. In the gene search interface enter `OsMADS50` in the search box and select the matching gene.
   1. The Homology tab loads an interactive TBrowse gene family tree, with branches expanded to show OsMADS50. The MSA zone shows InterPro domain annotations, and a gene neighborhood zone shows the genomic context surrounding the gene family members.
   2. The Pathways tab illustrates the role of this gene in various biochemical processes.
   3. The Papers tab lists publications describing the gene or pathway members
   4. The Expression tab assembles gene expression profiles from multiple studies across a variety of tissues. The Paralogs tab lets users compare baseline or differential expression profiles across the gene family members. An embedded eFP browser offers additional views of OsMADS50 expression.
   5. The Location tab shows a lightweight embedded genome browser and links to the full featured Ensembl browser.
   6. The Sequences tab provide access to gene, transcript, and peptide sequences for the gene model.
   7. The Germplasm tab shows accessions with predicted loss-of-function alleles for variants within the gene model.
3. From the *Location* tab, follow the link to the ensembl site to access the gene page
4. From the gene page, click on a transcript ID and load the [AlphaFold predicted model](http://oryza-ensembl-dev.gramene.org/Oryza_sativa/Transcript/AFDB?db=core;g=Os03g0122600;r=3:1270320-1300273;t=Os03t0122600-01).
5. To locate a gene based on a query sequence rather than a gene name, run [BLAST](http://oryza-ensembl-dev.gramene.org/Oryza_sativa/Tools/Blast) against a reference to jump to the region.


## Access & cite

The 19K-RGP rice resources are now live at [oryza19k.gramene.org](https://oryza19k.gramene.org) (reviewer credentials provided to the editor), moving to public, login-free production endpoints at publication. The durable variant archive is the [European Variation Archive (PRJEB105137)](https://www.ebi.ac.uk/eva/?eva-study=PRJEB105137).

Cite:

- Olson *et al.* Gramene 2025: expanded comparative genomics and pathway resources, integrated search, and pan-genome portals for crop research, Nucleic Acids Research, Volume 54, Issue D1, 6 January 2026, Pages D1720–D1732, [https://doi.org/10.1093/nar/gkaf1260](https://doi.org/10.1093/nar/gkaf1260)
- Wei *et al.* GrameneOryza: a comprehensive resource for Oryza genomes, genetic variation, and functional data, Database, Volume 2025, 2025, baaf021, [https://doi.org/10.1093/database/baaf021](https://doi.org/10.1093/database/baaf021)
