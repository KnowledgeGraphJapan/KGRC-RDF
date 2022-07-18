[Japanese](https://github.com/KnowledgeGraphJapan/KGRC-RDF/blob/master/2019/SPARQLsample_ja.md)

# Example Queries
Example SPARQL queries for the knowledge graphs of the Knowledge Graph Reasoning Challenge.

SPARQL endpoint is [http://kg.hozo.jp/fuseki/kgrc2020v2/sparql](http://kg.hozo.jp/fuseki/kgrc2020v2/sparql)

## Get hasPredicate (predicate representing the content of the scene) for scene 36 of "Speckled Band."
```
select ?o
{<http://kgc.knowledge-graph.jp/data/SpeckledBand/36> <http://kgc.knowledge-graph.jp/ontology/kgc.owl#hasPredicate> ?o .}
```
[View the results](http://kg.hozo.jp/fuseki/kgrc2020v2/sparql?query=select%20?o%0A%7B%3Chttp://kgc.knowledge-graph.jp/data/SpeckledBand/36%3E%20%3Chttp://kgc.knowledge-graph.jp/ontology/kgc.owl%23hasPredicate%3E%20?o%20.%7D)

## Get the contents (triple list) of the specified scene (e.g., scene 36 of "Speckled Band") 
```
select ?p ?o
{<http://kgc.knowledge-graph.jp/data/SpeckledBand/36> ?p ?o .}
```
[View the results](http://kg.hozo.jp/fuseki/kgrc2020v2/sparql?query=select%20?p%20?o%0A%7B%3Chttp://kgc.knowledge-graph.jp/data/SpeckledBand/36%3E%20?p%20?o%20.%7D)

## Get a list of scenes
```
PREFIX rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT ?s 
WHERE{
?s rdf:type kgc:Situation .
}
```
[View the results](http://kg.hozo.jp/fuseki/kgrc2020v2/sparql?query=PREFIX%20rdf:%20%20%3Chttp://www.w3.org/1999/02/22-rdf-syntax-ns%23%3E%0APREFIX%20kgc:%20%3Chttp://kgc.knowledge-graph.jp/ontology/kgc.owl#%3E%0A%0ASELECT%20?s%20%0AWHERE%7B%0A?s%20rdf:type%20kgc:Situation%20.%0A%7D)

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
[View the results](http://kg.hozo.jp/fuseki/kgrc2020v2/sparql?query=PREFIX%20rdf:%20%20%3Chttp://www.w3.org/1999/02/22-rdf-syntax-ns%23%3E%0APREFIX%20kgc:%20%3Chttp://kgc.knowledge-graph.jp/ontology/kgc.owl#%3E%0A%0ASELECT%20?s%20%0AFROM%20%3Chttp://kgc.knowledge-graph.jp/data/DancingMen%3E%0AWHERE%7B%0A?s%20rdf:type%20kgc:Situation%20.%0A%7D)

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
[View the results](http://kg.hozo.jp/fuseki/kgrc2020v2/sparql?query=PREFIX%20rdf:%20%20%3Chttp://www.w3.org/1999/02/22-rdf-syntax-ns%23%3E%0APREFIX%20kgc:%20%3Chttp://kgc.knowledge-graph.jp/ontology/kgc.owl#%3E%0A%0ASELECT%20?s%20?sc%0AWHERE%7B%0A?s%20kgc:subject%09%3Chttp://kgc.knowledge-graph.jp/data/DancingMen/Qubit%3E%20;%0A%20%20%20kgc:source%20%20?sc.%0AFILTER(lang(?sc)=%22ja%22)%0A%7D)


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
[View the results](http://kg.hozo.jp/fuseki/kgrc2020v2/sparql?query=PREFIX%20rdf:%20%20%3Chttp://www.w3.org/1999/02/22-rdf-syntax-ns%23%3E%0APREFIX%20kgc:%20%3Chttp://kgc.knowledge-graph.jp/ontology/kgc.owl#%3E%0APREFIX%20dm:%20%3Chttp://kgc.knowledge-graph.jp/data/DancingMen/%3E%0A%0ASELECT%20?s%20?p%20?o%0AFROM%20%3Chttp://kgc.knowledge-graph.jp/data/DancingMen%3E%0AWHERE%7B%0A?s%20?p%20?o.%0A?s%20rdf:type%20kgc:Situation%20.%0A?o%20rdf:type%20kgc:Situation%20.%0A%7D)
