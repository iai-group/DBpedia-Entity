# DBpedia-entity

DBpedia-entity is a standard test collection for entity search, which has been is first released as  *(DBpedia-entity v1)* [1], and is further updated as *(DBpedia-entity v2)* in:

`Faegheh Hasibi, Fedor Nikolaev, Chenyan Xiong, Krisztian Balog, Kotov Alexander, Svein Erik Bratsberg, and Jamie Callan. 2017. DBpedia-Entity v2: A Test Collection for Entity Search. In Proceedings of the 40th international ACM SIGIR conference on Research and development in Information Retrieval (SIGIR ’17).`

This repository contains this collection, baseline runs, and other details about the DBpedia dump and indexing.

## Queries

The collection consists of a set of heterogeneous entity-bearing queries, categorized into four groups:

- `SemSearch_ES`: Named named entity queries; e.g., "brooklyn bridge" or "08 toyota tundra." 
- `INEX-LD`: IR-style keyword queries; e.g., “electronic music genres".
- `ListSearch`: Queries that seek a particular list of entities, e.g., “Professional sports teams in Philadelphia”.
- `QALD2`: Natural language questions; e.g., "Who is the mayor of Berlin?"
The queries of the first 3 categories are prefixed with their group name. The rest of the queries are categorized as *ListSearch* queries.

## Collection

DBpedia-entity v2 is built based on [DBpedia 2015-10 version](http://wiki.dbpedia.org/Downloads2015-10). The collection can be found under `collection/v2` and is organized as follows:

- `queries-v2.txt`: 467 queries, where each line contains a queryID and query text. 
- `queries-v2_stopped.txt`: The same queries, with removed stop patterns and punctuation marks. 
- `qrels-v2.txt`: Relevance judgments in standard TREC format.
- `folds/`: 5-folds of train-test queries to be used for cross-validation in supervised approaches. There exists a single file for each query category. If cross-validation is performed for all queries,  `folds/all_queries.json` should be used.

## Baselines runs

The `runs` contains all the baseline presented in the paper in TREC runfile format. These correspond to the runs reported in Table 2 of the paper. The supervised methods are suffixed with `v1` and `v2` are trained based on Qrels v1 and v2, respectively. 


## Citation

If using this collection in a publication, please cite the following paper:
<pre>
@inproceedings{Hasibi:2017:DTC,
	author = {Hasibi, Faegheh and Nikolaev, Fedor and Xiong, Chenyan and Balog, Krisztian and Bratsberg, Svein Erik, Kotov, Alexander and Callan, Jamie},
	booktitle = {Proceedings of the 40th international ACM SIGIR conference on Research and development in Information Retrieval},
	title = {DBpedia-Entity v2: A Test Collection for Entity Search},
	series = {SIGIR '17},
	year = {2017},
   publisher = {ACM}
}
</pre>

Please also include [http://tiny.cc/dbpedia-entity.](http://tiny.cc/dbpedia-entity.) as where the data is available in the citation.

## Acknowledgment

This research was supported by Norwegian Research Council, National Science Foundation (NSF) grant IIS-1422676, Google Faculty Research Award, and Allen Institute for Artificial Intelligence Student Fellowship.
We Thank Saeid Balaneshin, Jan R. Benetka, Heng Ding, Dario Garigliotti, Mehedi Hasan, Indira Kurmantayeva, and Shuo Zhang for their help with creating relevance judgements. 


## Contact

In case of questions, feel free to contact <faegheh.hasibi@ntnu.no> or <krisztian.balog@uis.no>.