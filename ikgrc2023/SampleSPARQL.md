# Sample SPARQL queries for IKGRC2023
These are samples to query Open Knowledge Graph for [The 1st International Knowledge Graph Reasoning Challenge 2023](https://ikgrc.org/2023/)
  
- SPARQL Endpoint 
http://knowledge-graph.jp/sparql-ikgrc.html  

## Get all triples of Scene#36 in "Speckled Band"
```
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT *
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  <http://kgc.knowledge-graph.jp/data/SpeckledBand/36> ?p ?o .
}
```


## Get <hasPredicate> of Scene#36 in "Speckled Band".
```
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT *
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  <http://kgc.knowledge-graph.jp/data/SpeckledBand/36> kgc:hasPredicate ?o .
}
```

## Get <subject> of Scene#36 in "Speckled Band".
```
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT *
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  <http://kgc.knowledge-graph.jp/data/SpeckledBand/36> kgc:subject ?o .
}
```
## Get all <hasPredicate> in "Speckled Band".
```
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT ?o
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  ?s kgc:hasPredicate ?o .
}
```
When you want to get need <hasPredicate> with scenes.
```
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT ?s ?o
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  ?s kgc:hasPredicate ?o .
}
```
## Get all <Situation> in "Speckled Band".
```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT *
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  ?s rdf:type kgc:Situation .
}
```
## Get all <scene> in "Speckled Band".
```
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT *
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  ?s rdf:type/rdfs:subClassOf kgc:Scene .
  ?s rdf:type ?o .
}
```
## Get all <scene> whose <hasPredicate> is "meet" form all stories.
```
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>
SELECT DISTINCT *
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
FROM <http://kgc.knowledge-graph.jp/data/DancingMen>
FROM <http://kgc.knowledge-graph.jp/data/ACaseOfIdentity>
FROM <http://kgc.knowledge-graph.jp/data/DevilsFoot>
FROM <http://kgc.knowledge-graph.jp/data/CrookedMan>
WHERE {
  ?s kgc:hasPredicate <http://kgc.knowledge-graph.jp/data/predicate/meet> .
}
```

## ｢まらだのひも」で場面間のつながりの一覧を取得する
```
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT *
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  ?s rdf:type/rdfs:subClassOf kgc:Scene .
  ?o rdf:type/rdfs:subClassOf kgc:Scene .
  ?s ?p ?o .
}
```
## 「まだらのひも」の各場面の説明文（日本語）一覧を取得
```
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>
SELECT DISTINCT *
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  ?s kgc:source ?o .
  FILTER(lang(?o)="ja")
}
```
その中で「ホームズ」という文字列が含むシーンに限定する．
```
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>
SELECT DISTINCT *
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  ?s kgc:source ?o .
  FILTER(lang(?o)="ja")
  FILTER(regex(?o,"ホームズ"))  
}
```

