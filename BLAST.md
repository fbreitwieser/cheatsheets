
Report taxonomy information in tabular fo

rmat (requires taxdb):
```
blastn -db refseq_genomic -num_threads 24 -query in.fa -outfmt '6 std sacc staxids sscinames scomnames stitle' -out res.m8
```

BLAST help: https://www.ncbi.nlm.nih.gov/books/NBK279684/

Outfmt 6 options:

|Name| |
|--|--|
| qseqid | Query Seq-id |
| qacc | Query accesion |
| sseqid | Subject Seq-id |
| sallseqid | All subject Seq-id(s), separated by a ';' |
| sacc | Subject accession |
| sallacc | All subject accessions |
| qstart | Start of alignment in query |
| qend | End of alignment in query |
| sstart | Start of alignment in subject |
| send | End of alignment in subject |
| qseq | Aligned part of query sequence |
| sseq | Aligned part of subject sequence |
| evalue | Expect value |
| bitscore | Bit score |
| score | Raw score |
| length | Alignment length |
| pident | Percentage of identical matches |
| nident | Number of identical matches |
| mismatch | Number of mismatches |
| positive | Number of positive-scoring matches |
| gapopen | Number of gap openings |
| gaps | Total number of gap |
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
