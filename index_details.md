# Index Details


The details of the DBpedia indcies used for generating the baseline runs of the DBpedia-Entity v2 collection (i.e., Table 2 of [1]) are described here.


### DBpedia files

The following files from [DBpedia 2015-10 dump](http://downloads.dbpedia.org/2015-10/core-i18n/en/) are indexed:

- `anchor_text_en.ttl`
- `article_categories_en.ttl`
- `disambiguations_en.ttl`
- `infobox_properties_en.ttl`
- `instance_types_transitive_en.ttl`
- `labels_en.ttl`
- `long_abstracts_en.ttl`
- `mappingbased_literals_en.ttl`
- `mappingbased_objects_en.ttl`
- `page_links_en.ttl`
- `persondata_en.ttl`
- `short_abstracts_en.ttl`	
- `transitive_redirects_en.ttl`

### Index settings

- Entities without the following predicates are not indexed:
    * `<rdfs:comment>` 
    * `<rdfs:label>` 
- All predicate values with URIs are resolved by replacing "_" with space; e.g., the URI `http://dbpedia.org/resource/As_We_May_Think` becomes "as we may think".

### Index fields

The following fields are used for constructing the index,  following the general approach outlined in [2]. All fields listed below contain unique phrases.


| Field | Description | Predicates | Notes |
| --- | --- | --- | --- |
| Names | Names of the entity | `<foaf:name>`, `<dbp:name>`, `<foaf:givenName>`, `<foaf:surname>`, `<dbp:officialName>`, `<dbp:fullname>`, `<dbp:nativeName>`, `<dbp:birthName>`, `<dbo:birthName>`, `<dbp:nickname>`, `<dbp:showName>`, `<dbp:shipName>`, `<dbp:clubname>`, `<dbp:unitName>`, `<dbp:otherName>`, `<dbo:formerName>`, `<dbp:birthname>`, `<dbp:alternativeNames>`, `<dbp:otherNames>`, `<dbp:names>`, `<rdfs:label>` | |
| Categories | Entity types | `<dcterms:subject>` | |
| Similar entity names | Entity  name variants | `!<dbo:wikiPageRedirects>`, `!<dbo:wikiPageDisambiguates>`, `<dbo:wikiPageWikiLinkText>` | `!` denotes reverse direction (i.e. `<o, p, s>`) | 
| Attributes | Literal attibutes of entity | All `<s, p, o>`, where *"o"* is a literal and *"p"* is not in *Names*, *Categories*, *Similar entity names*, and blacklist predicates.For each `<s, p, o>` triple, if `p matches <dbp:.*>` both *p* and *o* are stored (i.e. *"p o"* is indexed). | |
| Related entity names | URI relations of entity|  Similar to *Attributes* field, but *"o"* should be a URI. | |  


### Group-specific settings

The baseline runs of the DBpedia-Entity v2 collection [1] are generated using two indices, denoted as index *A* and *B*. These indices, built by two different research groups, share the above settings, but are different in the following aspects.
 

**Index A:**

  - A new field called "catchall" is used; it encompass the content of all other fields. Duplicate values are not removed in this field.

**Index B:**

 - Anchor texts (i.e. contents of `<dbo:wikiPageWikiLinkText>` predicate) are added to both "similar entity names" and "attributes" fields.
 - Entity URIs are resolved differently for the "related entity names" field. Names for related entities are extracted in the same way as it is done for "names" field (see predicates for "names" in the above table), but only one arbitrary name is used for each related entity.
 - Category URIs are resolved using `category_labels_en.ttl` file
 - Predicate URIs are resolved using `infobox_property_definitions_en.ttl` file. If a name for a predicate is not defined, a predicate is omitted.

 
----------------
 
[1] Faegheh Hasibi, Fedor Nikolaev, Chenyan Xiong, Krisztian Balog, Svein Erik Bratsberg, Alexander Kotov, and Jamie Callan. 2017. “DBpedia-Entity v2: A Test Collection for Entity Search”, In proceedings of 40th ACM SIGIR conference on Research and Development in Information Retrieval (SIGIR ’17). 1265-1268.

[2] Nikita Zhiltsov, Alexander Kotov, and Fedor Nikolaev. 2015. “Fielded Sequential Dependence Model for Ad-Hoc Entity Retrieval in the Web of Data”. In Proceedings of the 38th International ACM SIGIR Conference on Research and Development in Information Retrieval (SIGIR ‘15). 253–262.