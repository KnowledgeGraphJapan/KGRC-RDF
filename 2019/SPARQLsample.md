# サンプルクエリ
ナレッジグラフ推論チャレンジ2019用の「ナレッジグラフ」を対象としたSPARQLクエリのサンプルです．  

SPARQLエンドポイントは，http://lod.hozo.jp/repositories/kgc2019 です．

## ｢まらだのひも」の場面36のhasPredicate（その場面の内容を表す述語）を取得する
```
select ?o
{<http://kgc.knowledge-graph.jp/data/SpeckledBand/36> <http://kgc.knowledge-graph.jp/ontology/kgc.owl#hasPredicate> ?o .}
```
[クエリ結果を見る](http://lod.hozo.jp/repositories/kgc2019#query/d/select%20?o%0A%7B%3Chttp://kgc.knowledge-graph.jp/data/SpeckledBand/36%3E%20%3Chttp://kgc.knowledge-graph.jp/ontology/kgc.owl%23hasPredicate%3E%20?o%20.%7D)

## 指定した場面（例：｢まらだのひも」の場面36）の内容（トリプル一覧）を取得する
```
select ?p ?o
{<http://kgc.knowledge-graph.jp/data/SpeckledBand/36> ?p ?o .}
```
[クエリ結果を見る](http://lod.hozo.jp/repositories/kgc2019#query/d/select%20?p%20?o%0A%7B%3Chttp://kgc.knowledge-graph.jp/data/SpeckledBand/36%3E%20?p%20?o%20.%7D)

## 場面の一覧を取得する
```
PREFIX rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX kgc: <http://kgc.knowledge-graph.jp/ontology/kgc.owl#>

SELECT ?s 
WHERE{
?s rdf:type kgc:Situation .
}
```
[クエリ結果を見る](http://lod.hozo.jp/repositories/kgc2019#query/d/PREFIX%20rdf:%20%20%3Chttp://www.w3.org/1999/02/22-rdf-syntax-ns%23%3E%0APREFIX%20kgc:%20%3Chttp://kgc.knowledge-graph.jp/ontology/kgc.owl#%3E%0A%0ASELECT%20?s%20%0AWHERE%7B%0A?s%20rdf:type%20kgc:Situation%20.%0A%7D)

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
[クエリ結果を見る](http://lod.hozo.jp/repositories/kgc2019#query/d/PREFIX%20rdf:%20%20%3Chttp://www.w3.org/1999/02/22-rdf-syntax-ns%23%3E%0APREFIX%20kgc:%20%3Chttp://kgc.knowledge-graph.jp/ontology/kgc.owl#%3E%0A%0ASELECT%20?s%20%0AFROM%20%3Chttp://kgc.knowledge-graph.jp/data/DancingMen%3E%0AWHERE%7B%0A?s%20rdf:type%20kgc:Situation%20.%0A%7D)

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
[クエリ結果を見る](http://lod.hozo.jp/repositories/kgc2019#query/d/PREFIX%20rdf:%20%20%3Chttp://www.w3.org/1999/02/22-rdf-syntax-ns%23%3E%0APREFIX%20kgc:%20%3Chttp://kgc.knowledge-graph.jp/ontology/kgc.owl#%3E%0A%0ASELECT%20?s%20?sc%0AWHERE%7B%0A?s%20kgc:subject%09%3Chttp://kgc.knowledge-graph.jp/data/DancingMen/Qubit%3E%20;%0A%20%20%20kgc:source%20%20?sc.%0AFILTER(lang(?sc)=%22ja%22)%0A%7D)


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
[クエリ結果を見る](http://lod.hozo.jp/repositories/kgc2019#query/d/PREFIX%20rdf:%20%20%3Chttp://www.w3.org/1999/02/22-rdf-syntax-ns%23%3E%0APREFIX%20kgc:%20%3Chttp://kgc.knowledge-graph.jp/ontology/kgc.owl#%3E%0APREFIX%20dm:%20%3Chttp://kgc.knowledge-graph.jp/data/DancingMen/%3E%0A%0ASELECT%20?s%20?p%20?o%0AFROM%20%3Chttp://kgc.knowledge-graph.jp/data/DancingMen%3E%0AWHERE%7B%0A?s%20?p%20?o.%0A?s%20rdf:type%20kgc:Situation%20.%0A?o%20rdf:type%20kgc:Situation%20.%0A%7D)
