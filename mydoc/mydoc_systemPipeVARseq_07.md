---
title: Annotate filtered variants
keywords: 
last_updated: Sun May  1 20:44:33 2016
---

The function `variantReport` generates a variant report using
utilities provided by the `VariantAnnotation` package. The report for
each sample is written to a tabular file containing genomic context annotations
(_e.g._ coding or non-coding SNPs, amino acid changes, IDs of affected
genes, etc.) along with confidence statistics for each variant. The parameter
file `annotate_vars.param` defines the paths to the input and output
files which are stored in a new `SYSargs` instance. 

## Annotate filtered variants called by `GATK`


{% highlight r %}
library("GenomicFeatures")
args <- systemArgs(sysma="annotate_vars.param", mytargets="targets_gatk_filtered.txt")
txdb <- loadDb("./data/tair10.sqlite")
fa <- FaFile(systemPipeR::reference(args))
variantReport(args=args, txdb=txdb, fa=fa, organism="A. thaliana")
{% endhighlight %}

## Annotate filtered variants called by `BCFtools`


{% highlight r %}
args <- systemArgs(sysma="annotate_vars.param", mytargets="targets_sambcf_filtered.txt")
txdb <- loadDb("./data/tair10.sqlite")
fa <- FaFile(systemPipeR::reference(args))
variantReport(args=args, txdb=txdb, fa=fa, organism="A. thaliana")
{% endhighlight %}

## Annotate filtered variants called by `VariantTools`


{% highlight r %}
args <- systemArgs(sysma="annotate_vars.param", mytargets="targets_vartools_filtered.txt")
txdb <- loadDb("./data/tair10.sqlite")
fa <- FaFile(systemPipeR::reference(args))
variantReport(args=args, txdb=txdb, fa=fa, organism="A. thaliana")
{% endhighlight %}


