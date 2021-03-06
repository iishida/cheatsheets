# bioawk

[bioawk](https://github.com/lh3/bioawk) is really awesome but I barely know how to use awk so I always get confused on how to use it. Here are some examples.

## Filter a fasta file on the sequence id

Head of the file:

```
 Thu 16 Apr - 18:31  ~/data_lg/czbiohub-reference/ncbi/refseq/releases/refseq-release98-2020-02-06/vertebrate_mammalian 
 olga@lrrr  gunzip -c vertebrate_mammalian_concatenated.faa.gz| head                                 
 >NP_999413.2 corticosteroid 11-beta-dehydrogenase isozyme 1 isoform 1 [Sus scrofa]
MAFMKKYLLPILGIFLAYYYYSANEEFRPEMLRGKKVIVTGASKGIGREMAYHLARMGAHVVVTARSEETLKKVVSHCLE
LGASSAHYVAGTMEDMTFAEQFVAKAGKLLGGLDMLILNHITHASMTPFSDDIHLVRRSMEVNFLSYVVLSVAALPMLKQ
SNGSIVVVSSQAGKMANPLVAPYSASKFALDGFFSSIRKEYSVTKVNVSITLCILGLIDTDTAMTAVAGILNVQPSPKEE
CALEIIKGAALRQEEVYYDSSILTSLLLGNPGRKILEFLSLRHYNMERFTNN
>NP_001335890.1 corticosteroid 11-beta-dehydrogenase isozyme 1 isoform 2 [Sus scrofa]
MRNSDQVVSHCLELGASSAHYVAGTMEDMTFAEQFVAKAGKLLGGLDMLILNHITHASMTPFSDDIHLVRRSMEVNFLSY
VVLSVAALPMLKQSNGSIVVVSSQAGKMANPLVAPYSASKFALDGFFSSIRKEYSVTKVNVSITLCILGLIDTDTAMTAV
AGILNVQPSPKEECALEIIKGAALRQEEVYYDSSILTSLLLGNPGRKILEFLSLRHYNMERFTNN
>XP_021111609.1 transferrin receptor protein 1 isoform X1 [Heterocephalus glaber]
```

Use `bioawk` to filter a gzipped fasta file for only fasta records whose name contains `NP_` ("good" records in NCBI that were manually curated):


```
 ✘  Thu 16 Apr - 18:28  ~/data_lg/czbiohub-reference/ncbi/refseq/releases/refseq-release98-2020-02-06/vertebrate_mammalian 
 olga@lrrr  gunzip -c  vertebrate_mammalian_concatenated.faa.gz \
 | head \
 | bioawk -c fastx ' { if ( $name ~ /NP_/ ) { print ">"$name" "$comment"\n"$seq } }'
>NP_999413.2 corticosteroid 11-beta-dehydrogenase isozyme 1 isoform 1 [Sus scrofa]
MAFMKKYLLPILGIFLAYYYYSANEEFRPEMLRGKKVIVTGASKGIGREMAYHLARMGAHVVVTARSEETLKKVVSHCLELGASSAHYVAGTMEDMTFAEQFVAKAGKLLGGLDMLILNHITHASMTPFSDDIHLVRRSMEVNFLSYVVLSVAALPMLKQSNGSIVVVSSQAGKMANPLVAPYSASKFALDGFFSSIRKEYSVTKVNVSITLCILGLIDTDTAMTAVAGILNVQPSPKEECALEIIKGAALRQEEVYYDSSILTSLLLGNPGRKILEFLSLRHYNMERFTNN
>NP_001335890.1 corticosteroid 11-beta-dehydrogenase isozyme 1 isoform 2 [Sus scrofa]
MRNSDQVVSHCLELGASSAHYVAGTMEDMTFAEQFVAKAGKLLGGLDMLILNHITHASMTPFSDDIHLVRRSMEVNFLSYVVLSVAALPMLKQSNGSIVVVSSQAGKMANPLVAPYSASKFALDGFFSSIRKEYSVTKVNVSITLCILGLIDTDTAMTAVAGILNVQPSPKEECALEIIKGAALRQEEVYYDSSILTSLLLGNPGRKILEFLSLRHYNMERFTNN
```
