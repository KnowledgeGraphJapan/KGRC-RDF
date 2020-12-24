# 推論チャレンジ2020用ナレッジグラフ【2020/12/24更新】 

[![CC BY 4.0][cc-by-shield]][cc-by]

ナレッジグラフ推論チャレンジ2020用のナレッジグラフを公開するレポジトリです．  

利用法については下記のサイトもご覧ください.  
https://challenge.knowledge-graph.jp/2020/rdf.html

## 2020/06/09 バージョン（5小説）＋ 2020/10/09 追加（2小説）  
- [2019年度版](https://github.com/KnowledgeGraphJapan/Challenge/tree/master/rdf/2019)の５小説について，不具合を大幅に修正したバージョンです（2020/06/09公開）．  
- [2020年度版] 「僧坊荘園（アベイ農場）」および「白銀号事件」を追加しました．  

## 2020/12/24版 バージョン　データ修正（6小説）＋ データ追加（1小説）  
- [2020年度(2020/10/09)版](https://github.com/KnowledgeGraphJapan/KGRC-RDF/tree/master/2020) で公開したナレッジグラフ（7小説分）のデータを見直し，修正を加えました．  
- 「入院患者」のナレッジグラフを追加しました．  

 
修正リクエストはGitHubのIsuuesおよびPull rewiestsで受け付けております。  
  
※現在，すべての小説について更なる見直し・修正作業を進めています．修正作業の終了後，データを更新予定ですが，現時点バージョンのデータ公開を継続します．  
  
SPARQLエンドポイント
- http://kg.hozo.jp/fuseki/kgrc2020v2/sparql (APIとして使う場合)
- http://knowledge-graph.jp/sparql2020v2.html (ブラウザから利用)  
※下記のグラフIRIをFROM句で指定する必要がありますのでご注意ください．
  
|小説|グラフIRI|
----|----
|まだらのひも|&lt;http://kgc.knowledge-graph.jp/data/SpeckledBand&gt;|
|踊る人形|&lt;http://kgc.knowledge-graph.jp/data/DancingMen&gt;|
|花婿失踪事件（同一事件）|&lt;http://kgc.knowledge-graph.jp/data/ACaseOfIdentity&gt;|
|悪魔の足|&lt;http://kgc.knowledge-graph.jp/data/DevilsFoot&gt;|
|背中の曲がった男（曲がれる者）|&lt;http://kgc.knowledge-graph.jp/data/CrookedMan&gt;|
|僧坊荘園（アベイ農場）|&lt;http://kgc.knowledge-graph.jp/data/AbbeyGrange&gt;|
|白銀号事件|&lt;http://kgc.knowledge-graph.jp/data/SilverBlaze&gt;|
|入院患者|&lt;http://kgc.knowledge-graph.jp/data/ResidentPatient&gt;|



## ライセンス
本データは人工知能学会セマンティックウェブとオントロジー研究会（SIG-SWO, JSAI）が，[クリエイティブ・コモンズ・ライセンス（表示4.0国際)](https://creativecommons.org/licenses/by/4.0/)のもとで提供しています．

[![CC BY 4.0][cc-by-image]][cc-by]

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg
