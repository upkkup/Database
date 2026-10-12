Time-focused Wikidata / Freebase knowledge extraction
=====================================================
1. pip install requests
2. python build_verified_knowledge.py --count 5000 --batch-size 40 --contact your-contact@example.com
3. Optional Freebase entity cross-check (large official RDF dump):
   python build_verified_knowledge.py --count 5000 --batch-size 40 --contact your-contact@example.com --freebase-rdf freebase-rdf-latest.gz

Outputs: knowledge.jsonl (JSON Lines, one {id,text} object per line), knowledge_provenance.jsonl (traceability).

IMPORTANT:
- Freebase MID from Wikidata P646 is a mapping, not proof that the fact exists in Freebase.
- --freebase-rdf checks whether mapped entities occur in the Freebase dump; it does not verify temporal triples. The provenance explicitly sets freebase_fact_verified=false.
- The script does not invent missing records; if network/API fails, it saves partial output and exits nonzero.
- Wikidata WDQS is a live database, not a pinned snapshot. Record the execution date for reproducibility.
- Avoid using any gold answers from evaluation datasets as source documents.
