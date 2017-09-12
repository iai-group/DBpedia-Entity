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
  - `annotator_agreements.tsv`: Inter-annotator agreements between crowd workers (and expert annotators, if applicable) for each query-entity pair. The agreement scores are computed according to the Fleiss' kappa index (i.e., Eq (3) of [its Wikipedia article](https://en.wikipedia.org/wiki/Fleiss%27_kappa)).

This repository also contains the **DBpedia-Entity v1** collection, which was built based on [DBpedia version 3.7](http://wiki.dbpedia.org/data-set-37). The collection can be found under `collection/v1` and is organized similar to the v2 version. There are, however, 3 qrels file for DBpedia-Entity v1:

- `qrels-v1_37.txt`: The original qrels, based on DBpedia 3.7.
- `qrels-v1_39.txt`: Qrels with updated entity IDs according to DBpedia 3.9.
- `qrels-v1_2015_10.txt`: Qrels with updated entity IDs according to DBpedia 2015-10.


## Baseline rankings

The `runs` folder contains a set of baseline rankings ("runs") in TREC format (the details of theindices used for generating these runs are described [here](index.rst)).

- `/v1`: The runs related to **DBpedia-Entity v1**, reported in Table 2 of the paper [2].
- `/v2`: The runs related to **DBpedia-Entity v2**, reported in the table below.  The evaluation metric is NDCG (Normalized Discounted Cumulative Gain) at ranks 10 and 100.  New retrieval systems, evaluated using DBpedia-Entity v2, are supposed to be compared against these results.

<table>
  <thead>
  <tr>
    <th>Model</th>
    <th colspan="2">SemSearch ES</th>
    <th colspan="2">INEX-LD</th>
    <th colspan="2">ListSearch</th>
    <th colspan="2">QALD-2</th>
    <th colspan="2">Total</th>
  </tr>
  <tr >
    <td></td>
    <td markdown="span">**@10**</td><td markdown="span">**@100**</td>
    <td markdown="span">**@10**</td><td markdown="span">**@100**</td>
    <td markdown="span">**@10**</td><td markdown="span">**@100**</td>
    <td markdown="span">**@10**</td><td markdown="span">**@100**</td>
    <td markdown="span">**@10**</td><td markdown="span">**@100**</td>
   </tr>
  </thead>
  <tbody>
  <tr>
	<td markdown="span">**BM25**</td >
	<td >0.2497</td><td >0.4110</td>
	<td >0.1828</td><td >0.3612</td>
	<td >0.0627</td><td >0.3302</td>
	<td >0.2751</td><td >0.3366</td>
	<td >0.2558</td><td >0.3582</td>
  </tr>
  <tr>
	<td markdown="span">**PRMS**</td >
	<td >0.5340</td><td >0.6108</td>
	<td >0.3590</td><td >0.4295</td>
	<td >0.3684</td><td >0.4436</td>
	<td >0.3151</td><td >0.4026</td>
	<td >0.3905</td><td >0.4688</td>
  </tr>
  <tr>
	<td markdown="span">**MLM-all**</td >
	<td >0.5528</td><td >0.6247</td>
	<td >0.3752</td><td >0.4493</td>
	<td >0.3712</td><td >0.4577</td>
	<td >0.3249</td><td >0.4208</td>
	<td >0.4021</td><td >0.4852</td>
  </tr>
  <tr>
	<td markdown="span">**LM**</td >
	<td >0.5555</td><td >0.6475</td>
	<td >0.3999</td><td >0.4745</td>
	<td >0.3925</td><td >0.4723</td>
	<td >0.3412</td><td >0.4338</td>
	<td >0.4182</td><td >0.5036</td>
  </tr>
  <tr style="border-bottom: 4px solid black">
  <td markdown="span">**SDM**</td >
	<td >0.5535</td><td >0.6672</td>
	<td >0.4030</td><td >0.4911 </td>
	<td >0.3961</td><td >0.4900</td>
	<td >0.3390</td><td >0.4274</td>
	<td >0.4185</td><td >0.5143</td>
  </tr>
  <tr>
	<td markdown="span">**LM+ELR**</td >
	<td >0.5554</td><td >0.6469</td>
	<td >0.4040</td><td >0.4816</td>
	<td >0.3992</td><td >0.4845</td>
	<td >0.3491</td><td >0.4383</td>
	<td >0.4230</td><td >0.5093</td>
  </tr>
  <tr>
	<td markdown="span">**SDM+ELR**</td >
	<td >0.5548</td><td >0.6680</td>
	<td >0.4104</td><td >0.4988</td>
	<td >0.4123</td><td >0.4992</td>
	<td >0.3446</td><td >0.4363</td>
	<td >0.4261</td><td >0.5211</td>
  </tr>
  <tr>
	<td markdown="span">**MLM-CA**</td >
	<td >0.6247</td><td >0.6854</td>
	<td >0.4029</td><td >0.4796</td>
	<td >0.4021</td><td >0.4786</td>
	<td >0.3365</td><td >0.4301</td>
	<td >0.4365</td><td >0.5143</td>
  </tr>
  <tr>
	<td markdown="span">**BM25-CA**</td >
	<td >0.5858</td><td >0.6883</td>
	<td >0.4120</td><td >0.5050</td>
	<td >0.4220</td><td markdown="span">**0.5142**</td>
	<td >0.3566</td><td >0.4426</td>
	<td >0.4399</td><td >0.5329 </td>
  </tr>
  <tr>
	<td markdown="span">**FSDM**</td >
	<td >0.6521</td><td >0.7220</td>
	<td >0.4214</td><td >0.5043</td>
	<td >0.4196</td><td >0.4952</td>
	<td >0.3401</td><td >0.4358</td>
	<td >0.4524</td><td >0.5342</td>
  </tr>
  <tr>
	<td markdown="span">**BM25F-CA**</td >
	<td >0.6281</td><td >0.7200</td>
	<td markdown="span">**0.4394**</td><td markdown="span">**0.5296**</td>
	<td markdown="span">**0.4252**</td><td >0.5106</td>
	<td markdown="span">**0.3689**</td><td markdown="span">**0.4614**</td>
	<td markdown="span">**0.4605**</td><td markdown="span">**0.5505**</td>
  </tr>
  <tr>
	<td markdown="span">**FSDM+ELR**</td >
	<td markdown="span">**0.6563**</td><td markdown="span">**0.7257**</td>
	<td >0.4354</td><td >0.5134</td>
	<td >0.4220</td><td >0.4985</td>
	<td >0.3468</td><td >0.4456</td>
	<td >0.4590</td><td >0.5408</td>
  </tr>
  </tbody>
</table>


## Citation

If you are using this collection, please cite the following paper:
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

## Acknowledgments

This research was partially supported by the Norwegian Research Council, National Science Foundation (NSF) grant IIS-1422676, Google Faculty Research Award, and Allen Institute for Artificial Intelligence Student Fellowship.
We Thank Saeid Balaneshin, Jan R. Benetka, Heng Ding, Dario Garigliotti, Mehedi Hasan, Indira Kurmantayeva, and Shuo Zhang for their help with creating relevance judgements.


## Contact

In case of questions, feel free to contact <faegheh.hasibi@ntnu.no> or <krisztian.balog@uis.no>.

----------------
[1] Krisztian Balog and Robert Neumayer. 2013. *"A Test Collection for Entity Search in DBpedia"*, In proceedings of 436th international ACM SIGIR conference on Research and development in Information Retrieval (SIGIR ’13). 737-740.

[2] Faegheh Hasibi, Fedor Nikolaev, Chenyan Xiong, Krisztian Balog, Svein Erik Bratsberg, Alexander Kotov, and Jamie Callan. 2017. *“DBpedia-Entity v2: A Test Collection for Entity Search”*, In proceedings of 40th ACM SIGIR conference on Research and Development in Information Retrieval (SIGIR ’17). 1265-1268.
