# The Learning experience of MMseq2
## Include：
### (1) Host annotation and result visualization of contigs with MMSeqs2
### (2) Clustering sequence data
### (3) Extract ORF
### (4) and so on ···
>->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->->
#### (1) Host annotation and result visualization of contigs with MMSeqs2

##### Step1:
```
# Before searching, you need to convert your FASTA file containing query sequences into a sequence DB（contigs.fasta-->queryDB）
Conmmands: 
mmseqs createdb <i:contigs.fasta> <o:queryDB>
mmseqs createdb  # module of MMseq2
<contigs.fasta>  # contigs file in FASTA format
<queryDB>  # sequence DB's prefix

Result：This step should generate eight files ：queryDB, queryDB_h and its corresponding index file queryDB.index
E：queryDB、queryDB.dbtype、queryDB.index、queryDB.lookup、queryDB.source、queryDB_h、queryDB_h.dbtype、queryDB_h.index
```
##### Step2:
```
# Make a seqTaxDB database that is a comparison database (take UniProtKB/Swiss-Prot as an example)
Conmmands:
mmseqs databases <i:database-name> <o:seqTaxDB-database> tmp
mmseqs databases  # module of MMseq2
<database-name>  # the database name in the table (database table on the official website)
<seqTaxDB-database>  # The prefix of converted seqTaxDB database
tmp  # process cache file
```
##### Step3:
```
# Taxonomy(annotate) contigs：
Conmmands:
mmseqs taxonomy <i:path/to/queryDB> <i:path/to/seqTaxDB> <o:taxonomyResult> tmp <--options>
mmseqs taxonomy  # module of MMseq2
<i:path/to/queryDB>  # step1's queryDB
<i:path/to/seqTaxDB>  # step2's seqTaxDB
<o:taxonomyResult>  # result file prefix
tmp  # process cache file
<options>  # other options
```
##### Step4:
```
# Convert result files to tsv format (i.e. format and consolidate all taxonomyResult.xxx files)
Commands:
mmseqs createtsv <i:path/to/queryDB> <i:taxonomyResult> <o:taxonomyResult.tsv>
mmseqs createtsv # module of MMseq2
<i:path/to/queryDB> # step1's queryDB
<i:taxonomyResult> # step'3 result file prefix
<o:taxonomyResult.tsv> # tsv格式的汇总文件
```
##### Step5:
```
# Annotation results can be converted to the Kraken result style
# The report file can be visualized in the [pavian](https://github.com/fbreitwieser/pavian)
Commands:
mmseqs taxonomyreport <i:path/to/seqTaxDB> <i:taxonomyResult> <o:taxonomyResult_report>
mmseqs taxonomyreport # module of MMseq2
<i:path/to/seqTaxDB>  # step2's seqTaxDB
<i:taxonomyResult> # step'3 result file prefix
<o:taxonomyResult_report> # annotated result file for Kraken result style
```
##### Step6:
```
# Result visualization (generate html file)
Commands:
mmseqs taxonomyreport <i:path/to/seqTaxDB> <i:taxonomyResult> <o: report.html> <--options>
mmseqs taxonomyreport # module of MMseq2
<i:path/to/seqTaxDB>  # step2's seqTaxDB
<i:taxonomyResult> # step'3 result file prefix
<o: report.html> # visualize html files
```
