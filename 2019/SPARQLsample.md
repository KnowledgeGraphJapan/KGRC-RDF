[Japanese](https://github.com/KnowledgeGraphJapan/KGRC-RDF/blob/master/2019/SPARQLsample_ja.md)

# Example Queries
Example SPARQL queries for the knowledge graphs of the Knowledge Graph Reasoning Challenge.

SPARQL endpoint is [http://kg.hozo.jp/fuseki/kgrc2020v2/sparql](http://kg.hozo.jp/fuseki/kgrc2020v2/sparql)

## Get hasPredicate (predicate representing the content of the scene) for scene 36 of "Speckled Band."
```
select ?o
from <http://kgc.knowledge-graph.jp/data/SpeckledBand>
where
{<http://kgc.knowledge-graph.jp/data/SpeckledBand/36> <http://kgc.knowledge-graph.jp/ontology/kgc.owl#hasPredicate> ?o .}
```
[View the results](http://kg.hozo.jp/fuseki/kgrc2020v2/sparql?query=select%20%3Fo%20%0Afrom%20%3Chttp%3A%2F%2Fkgc.knowledge-graph.jp%2Fdata%2FSpeckledBand%3E%0Awhere%0A%7B%3Chttp%3A%2F%2Fkgc.knowledge-graph.jp%2Fdata%2FSpeckledBand%2F36%3E%20%3Chttp%3A%2F%2Fkgc.knowledge-graph.jp%2Fontology%2Fkgc.owl%23hasPredicate%3E%20%3Fo%20.%7D&format=application%2Fjson)

## Get the contents (triple list) of the specified scene (e.g., scene 36 of "Speckled Band") 
```
select ?p ?o
from <http://kgc.knowledge-graph.jp/data/SpeckledBand>
where
{<http://kgc.knowledge-graph.jp/data/SpeckledBand/36> ?p ?o .}
```
[View the results](http://kg.hozo.jp/fuseki/kgrc2020v2/sparql?query=select%20%3Fp%20%3Fo%0Afrom%20%3Chttp%3A%2F%2Fkgc.knowledge-graph.jp%2Fdata%2FSpeckledBand%3E%0Awhere%20%7B%20%3Chttp%3A%2F%2Fkgc.knowledge-graph.jp%2Fdata%2FSpeckledBand%2F36%3E%20%3Fp%20%3Fo%20.%20%7D&format=application%2Fjson)

## Get a list of scenes
```
PREFIX rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT ?s 
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE{
?s rdf:type kgc:Situation .
}
```
[View the results](http://kg.hozo.jp/fuseki/kgrc2020v2/sparql?query=PREFIX%20rdf%3A%20%20%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0APREFIX%20kgc%3A%20%3Chttp%3A%2F%2Fkgc.knowledge-graph.jp%2Fontology%2Fkgc.owl%23%3E%0A%0ASELECT%20%3Fs%20%0AFROM%20%3Chttp%3A%2F%2Fkgc.knowledge-graph.jp%2Fdata%2FSpeckledBand%3E%0AWHERE%7B%0A%3Fs%20rdf%3Atype%20kgc%3ASituation%20.%0A%7D&format=application%2Fjson)

This SPARQL endpoint contains data for eight novels, so if you want to retrieve data only for a specific novel, specify the graph IRI of the novel to be retrieved as in `FROM <>`. 

## Get a list of scenes (search target is limited to "The Dancing Men") 
```
PREFIX rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT ?s 
FROM <http://kgc.knowledge-graph.jp/data/DancingMen>
WHERE{
?s rdf:type kgc:Situation .
}
```
[View the results](http://kg.hozo.jp/fuseki/kgrc2020v2/sparql?query=PREFIX%20rdf%3A%20%20%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0APREFIX%20kgc%3A%20%3Chttp%3A%2F%2Fkgc.knowledge-graph.jp%2Fontology%2Fkgc.owl%23%3E%0A%0ASELECT%20%3Fs%20%0AFROM%20%3Chttp%3A%2F%2Fkgc.knowledge-graph.jp%2Fdata%2FDancingMen%3E%0AWHERE%7B%0A%3Fs%20rdf%3Atype%20kgc%3ASituation%20.%0A%7D&format=application%2Fjson)

## Get a list of scenes that satisfy the conditions.
```
PREFIX rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT ?s ?sc
WHERE{
?s kgc:subject	<http://kgc.knowledge-graph.jp/data/DancingMen/Qubit> ;
   kgc:source  ?sc.
FILTER(lang(?sc)="ja")
}
```
[View the results](http://kg.hozo.jp/fuseki/kgrc2020v2/sparql?query=PREFIX%20rdf%3A%20%20%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0APREFIX%20kgc%3A%20%3Chttp%3A%2F%2Fkgc.knowledge-graph.jp%2Fontology%2Fkgc.owl%23%3E%0A%0ASELECT%20%3Fs%20%3Fsc%0AFROM%20%3Chttp%3A%2F%2Fkgc.knowledge-graph.jp%2Fdata%2FDancingMen%3E%0AWHERE%7B%0A%3Fs%20kgc%3Asubject%09%3Chttp%3A%2F%2Fkgc.knowledge-graph.jp%2Fdata%2FDancingMen%2FQubit%3E%20%3B%0A%20%20%20kgc%3Asource%20%20%3Fsc.%0AFILTER(lang(%3Fsc)%3D%22en%22)%0A%7D&format=application%2Fjson)


## Get connections between scenes
```
PREFIX rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>
PREFIX dm: <http://kgc.knowledge-graph.jp/data/DancingMen/>

SELECT ?s ?p ?o
FROM <http://kgc.knowledge-graph.jp/data/DancingMen>
WHERE{
?s ?p ?o.
?s rdf:type kgc:Situation .
?o rdf:type kgc:Situation .
}
```
[View the results](http://kg.hozo.jp/fuseki/kgrc2020v2/sparql?query=PREFIX%20rdf%3A%20%20%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0APREFIX%20kgc%3A%20%3Chttp%3A%2F%2Fkgc.knowledge-graph.jp%2Fontology%2Fkgc.owl%23%3E%0APREFIX%20dm%3A%20%3Chttp%3A%2F%2Fkgc.knowledge-graph.jp%2Fdata%2FDancingMen%2F%3E%0A%0ASELECT%20%3Fs%20%3Fp%20%3Fo%0AFROM%20%3Chttp%3A%2F%2Fkgc.knowledge-graph.jp%2Fdata%2FDancingMen%3E%0AWHERE%7B%0A%3Fs%20%3Fp%20%3Fo.%0A%3Fs%20rdf%3Atype%20kgc%3ASituation%20.%0A%3Fo%20rdf%3Atype%20kgc%3ASituation%20.%0A%7D&format=application%2Fjson)
