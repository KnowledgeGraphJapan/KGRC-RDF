# 「まだらの紐」（SpeckledBand）のナレッジグラフ
ナレッジグラフ推論チャレンジ2018用に作成したナレッジグラフです．<br>
本ナレッジグラフは，[青空文庫「まだらのひも」](https://www.aozora.gr.jp/cards/000009/card50717.html)   
を元に作成しました．

## ライセンス
本データは人工知能学会セマンティックウェブとオントロジー研究会（SIG-SWO, JSAI）が，[クリエイティブ・コモンズ・ライセンス（表示4.0国際)](https://creativecommons.org/licenses/by/4.0/)のもとで提供しています．


## 元データ
RDFに変換するために作成したテンプレートに記入した元データです．
- Speckled Band_Soruce.docx:原文からRDF化する部分をマーク（赤字）＋該当箇所を要約（青字）したもの
- SpeckledBand.xlsx
- SpeckledBand.tsv

## RDFデータ
- SpeckledBand.nt
- SpeckledBand.rdf
- SpeckledBand.ttl
- kgc.owl スキーマ定義（各RDFファイルにも含まれています）

## SPARQLエンドポイント
http://lod.hozo.jp/repositories/kgc
- WebブラウザでSPARQLクエリを試すには，*Queries*メニューを利用してください．
- プログラムからのSPARQLクエリには，上記アドレスをそのままお使いください．

## 参照解決可能URL
http://kgc.knowledge-graph.jp/data/SpeckledBand/XXX  （XXX=1から401の数字，または，k001）  
というURLにより，RDFデータに参照解決可能なアクセスができます.  
拡張子を変更することで，各種形式のRDFを取得できます．   
※この公開には，[Simple Linked Open Data Interface](https://github.com/uedayou/simplelodi)を利用しています．   
例）
 - http://kgc.knowledge-graph.jp/data/SpeckledBand/36
 - http://kgc.knowledge-graph.jp/data/SpeckledBand/36.ttl
 - http://kgc.knowledge-graph.jp/data/SpeckledBand/36.rdf
 - http://kgc.knowledge-graph.jp/data/SpeckledBand/36.json
 - http://kgc.knowledge-graph.jp/data/SpeckledBand/36.jsonld 

## 可視化ツール
http://knowledge-graph.jp/visualization/

## サンプルクエリ
http://challenge.knowledge-graph.jp/sparql.html
