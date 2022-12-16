# サンプルクエリ
ナレッジグラフ推論チャレンジ2020用の「ナレッジグラフ」を対象としたSPARQLクエリのサンプルです．  

SPARQLエンドポイントは，http://knowledge-graph.jp/sparql2020v2.html です．

## ｢まらだのひも」の場面36のhasPredicate（その場面の内容を表す述語）を取得する
```
select ?o
{<http://kgc.knowledge-graph.jp/data/SpeckledBand/036> <http://kgc.knowledge-graph.jp/ontology/kgc.owl#hasPredicate> ?o .}
```

## 指定した場面（例：｢まらだのひも」の場面36）の内容（トリプル一覧）を取得する
```
select ?p ?o
{<http://kgc.knowledge-graph.jp/data/SpeckledBand/036> ?p ?o .}
```

## 場面の一覧を取得する
```
PREFIX rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT ?s 
WHERE{
?s rdf:type kgc:Situation .
}
```

なお，このSPARQLエンドポイントには5つの小説のデータが入っていますので，特定の小説のデータのみを取得したい場合は`FROM <>`のように検索対象とする小説のグラフIRIを指定してください．

## 場面の一覧を取得する（検索対象を「踊る人形」に限定）
```
PREFIX rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT ?s 
FROM <http://kgc.knowledge-graph.jp/data/DancingMen>
WHERE{
?s rdf:type kgc:Situation .
}
```

## 条件を満たす場面の一覧を取得する
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


## 場面間のつながりを取得する
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
