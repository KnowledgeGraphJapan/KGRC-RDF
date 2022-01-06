# ナレッジグラフ推論チャレンジ用SPARQLクエリのサンプル
[人工知能学会SWO研究会ワークショップ「ナレッジグラフ推論チャレンジ2020技術勉強会」](https://kgrc2020ws.peatix.com/)で紹介した（※），
SPARQLクエリを元に一部の修正を加えたサンプル です．  

※勉強会での説明資料は[こちら](https://github.com/KnowledgeGraphJapan/LOD-ws-2020/blob/master/kgrc2020ws/KGRC-WS-ChallengIntro-KG-Schema_2020-0909.pdf)をご覧ください．  
  
サンプルクエリを実行するには，
- SPARQLエンドポイント  
http://knowledge-graph.jp/sparql2020v2.html  
  
にクエリをコピー＆貼り付けして，実行してください．


## ｢まらだのひも」の場面36の全トリプル（述語・目的語）を取得する
```
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT *
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  <http://kgc.knowledge-graph.jp/data/SpeckledBand/36> ?p ?o .
}
```


## ｢まらだのひも」の場面36のhasPredicate（その場面の内容を表す述語）を取得する
```
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT *
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  <http://kgc.knowledge-graph.jp/data/SpeckledBand/36> kgc:hasPredicate ?o .
}
```

## ｢まらだのひも」の場面36のsubject（その場面の主語）を取得する
```
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT *
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  <http://kgc.knowledge-graph.jp/data/SpeckledBand/36> kgc:subject ?o .
}
```
## ｢まらだのひも」で用いられているhasPredicate（その場面の内容を表す述語）の一覧を取得する
```
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT ?o
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  ?s kgc:hasPredicate ?o .
}
```
取得した「述語」が用いられている「場面」も合わせて取得したい場合は下記のクエリを用いる．
```
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT ?s ?o
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  ?s kgc:hasPredicate ?o .
}
```
## ｢まらだのひも」のSituation（事実・状況の描写）の一覧を取得する
```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT *
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  ?s rdf:type kgc:Situation .
}
```
## ｢まらだのひも」の全場面の一覧を取得する
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
## ｢全小説」で述語がmeetの場面の一覧を取得する
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
## ｢まらだのひも」で用いられているhasProperty（その場面の内容を表す状態）の一覧を取得する
```
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT ?o
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  ?s kgc:hasProperty ?o .
}
```
取得した「状態」が用いられている「場面」も合わせて取得したい場合は下記のクエリを用いる．
```
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT DISTINCT ?s ?o
FROM <http://kgc.knowledge-graph.jp/data/SpeckledBand>
WHERE {
  ?s kgc:hasProperty ?o .
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
