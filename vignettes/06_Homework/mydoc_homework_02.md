---
title: HW2 - Introduction to Biocluster and Linux
last_updated: 07-Mar-16
---

## Topic: Linux Basics

(1) Download Halobacterium proteome and inspect it
{% highlight sh %}
wget http://biocluster.ucr.edu/~tgirke/Linux.sh # downloads code from this slide
module load ncbi-blast/2.2.26
wget ftp://ftp.ncbi.nlm.nih.gov/genomes/genbank/archaea/Halobacterium_salinarum/representative/GCA_000069025.1_ASM6902v1/GCA_000069025.1_ASM6902v1_protein.faa.gz
gunzip GCA_000069025.1_ASM6902v1_protein.faa.gz
mv GCA_000069025.1_ASM6902v1_protein.faa halobacterium.faa
less halobacterium.faa # press q to quit
{% endhighlight %}

(2) How many protein sequences are stored in the downloaded file?
{% highlight sh %}
grep '>' halobacterium.faa | wc
grep '^>' halobacterium.faa --count
{% endhighlight %}

(3) How many proteins contain the pattern `WxHxxH` or `WxHxxHH`?
{% highlight sh %}
egrep 'W.H..H{1,2}' halobacterium.faa --count
{% endhighlight %}

(4) Use `less` to find IDs for pattern matches or use `awk`
{% highlight sh %}
awk --posix -v RS='>' '/W.H..(H){1,2}/ { print ">" $0;}' halobacterium.faa | less
awk --posix -v RS='>' '/W.H..(H){1,2}/ { print ">" $0;}' halobacterium.faa | grep '^>' | cut -c 2- | cut -f 1 -d\ > myIDs
{% endhighlight %}

(5) Create a BLASTable database with `formatdb`
{% highlight sh %}
formatdb -i halobacterium.faa -p T -o
{% endhighlight %}

(6) Query BLASTable database by IDs stored in a file (_e.g._ `myIDs`)
{% highlight sh %}
fastacmd -d halobacterium.faa -i myIDs > myseq.fasta
{% endhighlight %}

(7) Run BLAST search for sequences stored in `myseq.fasta`
{% highlight sh %}
blastall -p blastp -i myseq.fasta -d halobacterium.faa -o blastp.out -e 1e-6 -v 10 -b 10
blastall -p blastp -i myseq.fasta -d halobacterium.faa -m 8 -e 1e-6 > blastp.tab
{% endhighlight %}

Additional exercise material in [Linux Manual](http://manuals.bioinformatics.ucr.edu/home/linux-basics#TOC-Exercises)

## Homework assignment

Perform above analysis on the following _Escherichia coli_ strain: ftp://ftp.ncbi.nih.gov/genomes/genbank/bacteria/Escherichia_coli/latest_assembly_versions/GCA_000461395.1_Esch_coli_UMEA_3592-1_V1/GCA_000461395.1_Esch_coli_UMEA_3592-1_V1_protein.faa.gz. 
Record result from final BLAST command (with `-m 8`) in text file.

## Homework submission

Upload result file to your private course GitHub repository under `Homework/HW2/HW2.txt`.

## Due date

Most homeworks will be due one week after they are assigned. This one is due on Thu, April 7th at 6:00 PM.
