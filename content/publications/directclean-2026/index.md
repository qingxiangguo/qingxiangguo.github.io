---
title: "DirectClean: artifact-aware preprocessing and read rescue for Oxford Nanopore direct-cDNA transcriptome sequencing"
authors:
  - me
  - "Yangyang Li"
  - "Rendong Yang"
date: "2026-10-31T00:00:00Z"
publishDate: "2026-10-31T00:00:00Z"
publication_types: ["article-journal"]
publication: "*NAR Genomics and Bioinformatics*, 8(4): lqag132"
publication_short: "NAR Genom. Bioinform."
featured: true
doi: "10.1093/nargab/lqag132"
abstract: |
  Oxford Nanopore direct-cDNA sequencing enables full-length transcriptome profiling without PCR amplification, but recurrent chimeric artifacts introduced during reverse transcription and library preparation can compromise isoform reconstruction and gene-fusion analysis. These include foldback inversions, aberrant primer configurations, internal adapter concatemers, and homopolymer-mediated template-switching events. Existing preprocessing strategies primarily address primer-based orientation and adapter detection, leaving several direct-cDNA-specific artifact classes unresolved and often discarding reads that still contain usable transcript sequence. We developed DirectClean, an artifact-aware preprocessing and read-rescue framework integrating strand orientation, artifact removal, and junction-level splitting of recoverable chimeric reads. Benchmarking across four direct-cDNA datasets showed consistently higher read and base retention with DirectClean than with Pychopper. In VCaP, DirectClean retained 65.2% of reads compared with 57.6% for Pychopper, supported additional transcripts, and reduced the chimeric read rate from 30.9% in raw data to 16.9%. Semi-synthetic validation demonstrated accurate rescue of adapter-associated and A/T-rich chimeric reads, and matched real-data analyses showed no enrichment of novel transcript models in split-derived reads relative to matched untouched reads. DirectClean provides a reproducible, openly available framework for artifact-aware preprocessing of direct-cDNA transcriptomes and improves the reliability of downstream isoform and fusion analyses.
summary: "DirectClean detects and resolves ONT direct-cDNA sequencing artifacts while rescuing usable read sequences, improving read retention and downstream transcriptome analysis."
tags:
  - Nanopore
  - Direct-cDNA sequencing
  - Read rescue
  - Chimera artifacts
  - Bioinformatics software
image:
  filename: featured.jpg
---

**Editor's Choice** · *NAR Genomics and Bioinformatics* (2026)

**Official Publication:** https://doi.org/10.1093/nargab/lqag132  
**Code:** https://github.com/ylab-hi/DirectClean
