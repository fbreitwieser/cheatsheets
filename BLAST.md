
Report taxonomy information in tabular format (requires taxdb):
```
blastn -db refseq_genomic -num_threads 24 -query in.fa -outfmt '6 std sacc staxids sscinames scomnames stitle' -out res.m8
```

BLAST help: https://www.ncbi.nlm.nih.gov/books/NBK279684/

Outfmt 6 `std` options:

|Position|Name| Description|
|--|--|--|
|1| qseqid | Query Seq-id |
|2| sseqid | Subject Seq-id |
|3| pident | Percentage of identical matches |
|4| length | Alignment length |
|5| mismatch | Number of mismatches |
|6| gapopen | Number of gap openings |
|7| qstart | Start of alignment in query |
|8| qend | End of alignment in query |
|9| sstart | Start of alignment in subject |
|10| send | End of alignment in subject |
|11| evalue | Expect value |
|12| bitscore | Bit score |

Additional columns:

| Specifier | Description |
|--|--|
| qacc | Query accesion |
| sacc | Subject accession |
| sallacc | All subject accessions |
| sallseqid | All subject Seq-id(s), separated by a ';' |
| qseq | Aligned part of query sequence |
| sseq | Aligned part of subject sequence |
| nident | Number of identical matches |
| positive | Number of positive-scoring matches |
| gaps | Total number of gap |
| score | Raw score |
| ppos | Percentage of positive-scoring matches |
| frames | Query and subject frames separated by a '/' |
| qframe | Query frame |
| sframe | Subject frame |
| btop | Blast traceback operations (BTOP) |
| staxids | unique Subject Taxonomy ID(s), separated by a ';'(in numerical order) |
| sscinames | unique Subject Scientific Name(s), separated by a ';' |
| scomnames | unique Subject Common Name(s), separated by a ';' |
| sblastnames | unique Subject Blast Name(s), separated by a ';' (in alphabetical order) |
| sskingdoms | unique Subject Super Kingdom(s), separated by a ';' (in alphabetical order) |
| stitle | Subject Title |
| salltitles | All Subject Title(s), separated by a '<>' |
| sstrand | Subject Strand |
| qcovs | Query Coverage Per Subject (for all HSPs) |
| qcovhsp | Query Coverage Per HSP |

When not provided, the default value is:
'qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore', which is equivalent to the keyword 'std'

## Building custom database
```
makeblastdb -in mydb.fsa -parse_seqids -dbtype {nucl,prot}
```

## Extracting FASTA from database

Extract all human sequences from the nr database
```
$ blastdbcmd -db nr -entry all -outfmt "%g %T" | \
   awk ' { if ($2 == 9606) { print $1 } } ' | \
   blastdbcmd -db nr -entry_batch - -out human_sequences.txt
```

https://www.ncbi.nlm.nih.gov/books/NBK279689/
