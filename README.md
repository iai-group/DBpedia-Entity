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

**DBpedia-entity v2** is built based on [DBpedia 2015-10 version](http://wiki.dbpedia.org/Downloads2015-10). The collection can be found under `collection/v2` and is organized as follows:

- `queries-v2.txt`: 467 queries, where each line contains a queryID and query text. 
- `queries-v2_stopped.txt`: The same queries, with removed stop patterns and punctuation marks. 
- `qrels-v2.txt`: Relevance judgments in standard TREC format.
- `folds/`: 5-folds of train-test queries to be used for cross-validation in supervised approaches. There exists a single file for each query category. If cross-validation is performed for all queries,  `folds/all_queries.json` should be used.

This repository also contains the **DBpedia-entity v1** collection, which was built based on [DBpedia 3.7 version](http://wiki.dbpedia.org/data-set-37). The collection can be found under `collection/v1` and is organized similar to the v2 version. There are, however, 3 qrels file for DBpedia-entity v2:

- `qrels-v1_37.txt`: The original qrels, based on DBpedia 3.7.
- `qrels-v1_39.txt`: Qrels with updated entity IDs according to DBpedia 3.9.
- `qrels-v1_2015_10.txt`: Qrels with updated entity IDs according to DBpedia 2015-10.



## Baselines runs

The `runs` contains all the baseline presented in the paper in TREC runfile format. The following runs are made available under the `runs` folder:

- `/v1`: The runs related to **DBpedia-entity v1**, reported in Table 2 of [2].
- `/v2`: The runs related to **DBpedia-entity v2**, reported on the following table. 

## Performance of baseline runs

The results of the baseline runs for *DBpedia-entity v2* with respect to NDCG at ranks 10 and 100 are reported in the following table.
Any new run on DBpedia-entity v2 may be compared to these results.

![alt text](https://github.com/iai-group/DBpedia-Entity/blob/master/results_table.png)

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
