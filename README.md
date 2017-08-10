# DBpedia-Entity

DBpedia-Entity is a standard test collection for entity search over the DBpedia knowledge base. It is meant for evaluating retrieval systems that return a ranked list of entities (DBpedia URIs) in response to a free text user query.

The first version of the collection (*DBpedia-Entity v1*) was released in 2013, based on DBpedia v3.7 [1].  It was created by assembling search queries from a number of entity-oriented benchmarking campaigns and mapping relevant results to DBpedia.
An updated version of the collection, *DBpedia-Entity v2*, has been released in 2017, as a result of a collaborative effort between the [IAI group](http://iai.group) of the University of Stavanger, the Norwegian University of Science and Technology, Wayne State University, and Carnegie Mellon University [2].
It has been published at the 40th International ACM SIGIR Conference on Research and Development in Information Retrieval (SIGIR'17), where it received a Best Short Paper Honorable Mention Award.  See the  [paper](http://hasibi.com/files/sigir2017-dbpedia_entity.pdf) and [poster](http://hasibi.com//files/posters/dbpedia-entity.pdf).


## Knowledge base

The test collection is based on [DBpedia version 2015-10](http://wiki.dbpedia.org/Downloads2015-10), specifically on the English subset.
We require entities to have both a title and abstract (i.e., `rdfs:label` and `rdfs:comment` predicates)--this effectively  filters out category, redirect, and disambiguation pages. Note that list pages, on the other hand, are retained.  In the end, there are 4.6 million entities, each uniquely identified by its URI.  We use a simplified prefixed format:  `http://dbpedia.org/resource/Albert_Einstein` => `<dbpedia:Albert_Einstein>`.


## Queries

The collection consists of a set of heterogeneous entity-bearing queries, assembled from various benchmarking campaigns (see the paper for details). Queries are categorized into four groups:

| Category | Description | Examples |
| --- | --- | --- |
| `SemSearch_ES` | Named entity queries | "brooklyn bridge", "08 toyota tundra" |
| `INEX-LD` | IR-style keyword queries | "electronic music genres" |
| `QALD2` | Natural language questions | "Who is the mayor of Berlin?" |
| `ListSearch` | Queries that seek a particular list of entities | "Professional sports teams in Philadelphia" |

All queries are prefixed with the name of the originating benchmark.  `SemSearch_ES`, `INEX-LD`, and `QALD2` each correspond to a separate category; the rest of the queries belong to the `ListSearch` category.


## Relevance judgments

Relevance judgments are collected using crowdsourcing. To ensure high quality, we obtained further expert annotations for cases with substantial disagreement.
In total, over 49K query-entity pairs are labeled using a three-point scale (0: irrelevant, 1: relevant, and 2: highly relevant).


## Files

The **DBpedia-Entity v2** collection can be found under `collection/v2` and is organized as follows:

  - `queries-v2.txt`: The set of 467 queries, where each line contains a query ID and query text pair.
  - `queries-v2_stopped.txt`: The same queries, with stop patterns and punctuation marks removed.
  - `qrels-v2.txt`: Relevance judgments in standard TREC format.
  - `folds/`: Partitioning of queries for 5-fold cross validation. This is provided to make results directly comparable by using the same partitioning for supervised approaches. A separate file is provided for each query subset; if training is done over the set of all queries, use the `all_queries.json` file.

This repository also contains the **DBpedia-Entity v1** collection, which was built based on [DBpedia version 3.7](http://wiki.dbpedia.org/data-set-37). The collection can be found under `collection/v1` and is organized similar to the v2 version. There are, however, 3 qrels file for DBpedia-Entity v1:

- `qrels-v1_37.txt`: The original qrels, based on DBpedia 3.7.
- `qrels-v1_39.txt`: Qrels with updated entity IDs according to DBpedia 3.9.
- `qrels-v1_2015_10.txt`: Qrels with updated entity IDs according to DBpedia 2015-10.


## Baseline rankings

The `runs` folder contains a set of baseline rankings ("runs") in TREC format:

- `/v1`: The runs related to **DBpedia-Entity v1**, reported in Table 2 of the paper [2].
- `/v2`: The runs related to **DBpedia-Entity v2**, reported in the table below.  The evaluation metric is NDCG (Normalized Discounted Cumulative Gain) at ranks 10 and 100.  New retrieval systems, evaluated using DBpedia-Entity v2, are supposed to be compared against these results.

![alt text](https://github.com/iai-group/DBpedia-Entity/blob/master/results_table.png)


## Related resources

  - [Entity Summarization](https://github.com/iai-group/DynamicEntitySummarization-DynES): 100 query-entity pairs (evenly distributed among the four query subsets) and graded judments for their corresponding entity facts.
  - [Target type annotations](https://github.com/iai-group/sigir2017-query_types): The same set of queries is annotated with target query types using the DBpedia Ontology.


## Citation

If you using this collection, please cite the following paper:
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

If possible, please also include the [http://tiny.cc/dbpedia-entity](http://tiny.cc/dbpedia-entity) URL in your paper.

## Acknowledgment

This research was partially supported by the Norwegian Research Council, National Science Foundation (NSF) grant IIS-1422676, Google Faculty Research Award, and Allen Institute for Artificial Intelligence Student Fellowship.
We Thank Saeid Balaneshin, Jan R. Benetka, Heng Ding, Dario Garigliotti, Mehedi Hasan, Indira Kurmantayeva, and Shuo Zhang for their help with creating relevance judgements.


## Contact

In case of questions, feel free to contact <faegheh.hasibi@ntnu.no> or <krisztian.balog@uis.no>.

----------------
[1] K. Balog and R. Neumayer. *“A Test Collection for Entity Search in DBpedia”*, In proceedings of 436th international ACM SIGIR conference on Research and development in Information Retrieval (SIGIR ’13), pages 737-740,  2013.

[2] F. Hasibi, F. Nikolaev, C. Xiong, K. Balog, S. E. Bratsberg, A. Kotov, and J. Callan. *“DBpedia-Entity v2: A Test Collection for Entity Search”*, In proceedings of 40th ACM SIGIR conference on Research and Development in Information Retrieval (SIGIR ’17),  2017.
