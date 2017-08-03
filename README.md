# DBpedia-Entity

DBpedia-Entity is a standard test collection for entity search, which has been first released as  *DBpedia-Entity v1* [1], and is further updated as *DBpedia-Entity v2* [2]. This repository contains the collection, baseline runs, and other details about the DBpedia dump and index.

For detailed information, please check the DBpedia-Entity v2 [paper](http://hasibi.com/files/sigir2017-dbpedia_entity.pdf) and [poster](http://hasibi.com//files/posters/dbpedia-entity.pdf).

## Queries

The collection consists of a set of heterogeneous entity-bearing queries, categorized into four groups:

- `SemSearch_ES`: Named entity queries; e.g., "brooklyn bridge" or "08 toyota tundra."
- `INEX-LD`: IR-style keyword queries; e.g., "electronic music genres".
- `QALD2`: Natural language questions; e.g., "Who is the mayor of Berlin?"
- `ListSearch`: Queries that seek a particular list of entities; e.g., "Professional sports teams in Philadelphia".

All queries are prefixed with the name of the originating benchmark.  `SemSearch_ES`, `INEX-LD`, and `QALD2` each correspond to a separate category; the rest of the queries belong to the `ListSearch` category.

## Collection

**DBpedia-Entity v2** is built based on [DBpedia version 2015-10](http://wiki.dbpedia.org/Downloads2015-10). The collection can be found under `collection/v2` and is organized as follows:

- `queries-v2.txt`: 467 queries, where each line contains a queryID and query text.
- `queries-v2_stopped.txt`: The same queries, with removed stop patterns and punctuation marks.
- `qrels-v2.txt`: Relevance judgments in standard TREC format.
- `folds/`: 5-folds of train-test queries for each query subset, to be used for cross-validation in supervised approaches. If cross-validation is performed for all queries,  `folds/all_queries.json` should be used.

This repository also contains the **DBpedia-Entity v1** collection, which was built based on [DBpedia version 3.7](http://wiki.dbpedia.org/data-set-37). The collection can be found under `collection/v1` and is organized similar to the v2 version. There are, however, 3 qrels file for DBpedia-Entity v1:

- `qrels-v1_37.txt`: The original qrels, based on DBpedia 3.7.
- `qrels-v1_39.txt`: Qrels with updated entity IDs according to DBpedia 3.9.
- `qrels-v1_2015_10.txt`: Qrels with updated entity IDs according to DBpedia 2015-10.


## Baselines runs

The `runs` folder contains all the baseline runs related to this collection in TREC format. The following runs are made available:

- `/v1`: The runs related to **DBpedia-Entity v1**, reported in Table 2 of [2].
- `/v2`: The runs related to **DBpedia-Entity v2**, reported in the following table. These runs are compared with respect to NDCG at ranks 10 and 100. Any new run on DBpedia-Entity v2 is supposed to be compared against these results.

![alt text](https://github.com/iai-group/DBpedia-Entity/blob/master/results_table.png)

## Citation

If using this collection in a publication, please cite the following paper:
<pre>
@inproceedings{Hasibi:2017:DVT,
 author =    {Hasibi, Faegheh and Nikolaev, Fedor and Xiong, Chenyan and Balog, Krisztian and Bratsberg, Svein Erik and Kotov, Alexander and Callan, Jamie},
 title =     {DBpedia-Entity V2: A Test Collection for Entity Search},
 booktitle = {Proceedings of the 40th International ACM SIGIR Conference on Research and Development in Information Retrieval},
 series =    {SIGIR '17},
 year =      {2017},
 pages =     {1265--1268},
 doi =       {10.1145/3077136.3080751},
 publisher = {ACM}
}
</pre>

If possible, please also include the [http://tiny.cc/dbpedia-entity](http://tiny.cc/dbpedia-entity) URL in your paper, where the data is available for download.

## Acknowledgment

This research was partialy supported by Norwegian Research Council, National Science Foundation (NSF) grant IIS-1422676, Google Faculty Research Award, and Allen Institute for Artificial Intelligence Student Fellowship.
We Thank Saeid Balaneshin, Jan R. Benetka, Heng Ding, Dario Garigliotti, Mehedi Hasan, Indira Kurmantayeva, and Shuo Zhang for their help with creating relevance judgements.


## Contact

In case of questions, feel free to contact <faegheh.hasibi@ntnu.no> or <krisztian.balog@uis.no>.

----------------
[1] K. Balog and R. Neumayer. *“A Test Collection for Entity Search in DBpedia”*, In proceedings of 436th international ACM SIGIR conference on Research and development in Information Retrieval (SIGIR ’13), pages 737-740,  2013.

[2] F. Hasibi, F. Nikolaev, C. Xiong, K. Balog, S. E. Bratsberg, A. Kotov, and J. Callan. *“DBpedia-Entity v2: A Test Collection for Entity Search”*, In proceedings of 40th ACM SIGIR conference on Research and Development in Information Retrieval (SIGIR ’17),  2017.
