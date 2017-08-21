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
    <td markdown="span"><b>@10</b></td><td ><b>@100</b></td>
    <td ><b>@10</b></td><td ><b>@100</b></td>
    <td ><b>@10</b></td><td ><b>@100</b></td>
    <td ><b>@10</b></td><td ><b>@100</b></td>
    <td ><b>@10</b></td><td ><b>@100</b></td>
   </tr>
  </thead>
  <tbody>
  <tr>
	<td ><b>BM25</b></td>
	<td >0.2497</td><td >0.4110</td>
	<td >0.1828</td><td >0.3612</td>
	<td >0.0627</td><td >0.3302</td>
	<td >0.2751</td><td >0.3366</td>
	<td >0.2558</td><td >0.3582</td>
  </tr>
  <tr>
	<td ><b>PRMS</b></td>
	<td >0.5340</td><td >0.6108</td>
	<td >0.3590</td><td >0.4295</td>
	<td >0.3684</td><td >0.4436</td>
	<td >0.3151</td><td >0.4026</td>
	<td >0.3905</td><td >0.4688</td>
  </tr>
  <tr>
	<td ><b>MLM-all</b></td>
	<td >0.5528</td><td >0.6247</td>
	<td >0.3752</td><td >0.4493</td>
	<td >0.3712</td><td >0.4577</td>
	<td >0.3249</td><td >0.4208</td>
	<td >0.4021</td><td >0.4852</td>
  </tr>
  <tr>
	<td ><b>LM</b></td>
	<td >0.5555</td><td >0.6475</td>
	<td >0.3999</td><td >0.4745</td>
	<td >0.3925</td><td >0.4723</td>
	<td >0.3412</td><td >0.4338</td>
	<td >0.4182</td><td >0.5036</td>
  </tr>
  <tr style="border-bottom: 4px solid black">
  <td ><b>SDM</b></td>
	<td >0.5535</td><td >0.6672</td>
	<td >0.4030</td><td >0.4911 </td>
	<td >0.3961</td><td >0.4900</td>
	<td >0.3390</td><td >0.4274</td>
	<td >0.4185</td><td >0.5143</td>
  </tr>
  <tr>
	<td ><b>LM+ELR</b></td>
	<td >0.5554</td><td >0.6469</td>
	<td >0.4040</td><td >0.4816</td>
	<td >0.3992</td><td >0.4845</td>
	<td >0.3491</td><td >0.4383</td>
	<td >0.4230</td><td >0.5093</td>
  </tr>
  <tr>
	<td ><b>SDM+ELR</b></td>
	<td >0.5548</td><td >0.6680</td>
	<td >0.4104</td><td >0.4988</td>
	<td >0.4123</td><td >0.4992</td>
	<td >0.3446</td><td >0.4363</td>
	<td >0.4261</td><td >0.5211</td>
  </tr>
  <tr>
	<td ><b>MLM-CA</b></td>
	<td >0.6247</td><td >0.6854</td>
	<td >0.4029</td><td >0.4796</td>
	<td >0.4021</td><td >0.4786</td>
	<td >0.3365</td><td >0.4301</td>
	<td >0.4365</td><td >0.5143</td>
  </tr>
  <tr>
	<td ><b>BM25-CA</b></td>
	<td >0.5858</td><td >0.6883</td>
	<td >0.4120</td><td >0.5050</td>
	<td >0.4220</td><td ><b>0.5142</b></td>
	<td >0.3566</td><td >0.4426</td>
	<td >0.4399</td><td >0.5329 </td>
  </tr>
  <tr>
	<td ><b>FSDM</b></td>
	<td >0.6521</td><td >0.7220</td>
	<td >0.4214</td><td >0.5043</td>
	<td >0.4196</td><td >0.4952</td>
	<td >0.3401</td><td >0.4358</td>
	<td >0.4524</td><td >0.5342</td>
  </tr>
  <tr>
	<td ><b>BM25F-CA</b></td>
	<td >0.6281</td><td >0.7200</td>
	<td ><b>0.4394</b></td><td ><b>0.5296</b></td>
	<td ><b>0.4252</b></td><td >0.5106</td>
	<td ><b>0.3689</b></td><td ><b>0.4614</b></td>
	<td ><b>0.4605</b></td><td ><b>0.5505</b></td>
  </tr>
  <tr>
	<td ><b>FSDM+ELR</b></td>
	<td ><b>0.6563</b></td><td ><b>0.7257</b></td>
	<td >0.4354</td><td >0.5134</td>
	<td >0.4220</td><td >0.4985</td>
	<td >0.3468</td><td >0.4456</td>
	<td >0.4590</td><td >0.5408</td>
  </tr>
  </tbody>
</table>

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
[1] Krisztian Balog and Robert Neumayer. 2013. *"A Test Collection for Entity Search in DBpedia"*, In proceedings of 436th international ACM SIGIR conference on Research and development in Information Retrieval (SIGIR ’13). 737-740.

[2] Faegheh Hasibi, Fedor Nikolaev, Chenyan Xiong, Krisztian Balog, Svein Erik Bratsberg, Alexander Kotov, and Jamie Callan. 2017. *“DBpedia-Entity v2: A Test Collection for Entity Search”*, In proceedings of 40th ACM SIGIR conference on Research and Development in Information Retrieval (SIGIR ’17). 1265-1268.
