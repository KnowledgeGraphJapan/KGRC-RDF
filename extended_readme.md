# VirtualHome2KGデータセット―家庭内の日常生活行動のシミュレーション動画とナレッジグラフ―

<table width="100%">
<tr>
<td width="49%"><img src="./asset/put_food_in_fridge1.gif" alt="video"></td>
<td width="51%"><img src="./asset/put_food_in_fridge1_kg.png" alt="kg"></td>
</tr>
</table>

## 簡単に言うと
- <b>家庭内日常生活を仮想空間でシミュレーションした動画と，その内容を表すナレッジグラフのセット</b>

## 目次
1. [背景](#背景)
2. [提案データセット](#提案データセット)
3. [データセットの構成](#データセットの構成)
4. [ナレッジグラフの説明](#ナレッジグラフの説明)
5. [ナレッジグラフの使用方法](#ナレッジグラフの使用方法)
6. [同様のナレッジグラフの作成方法](#同様のナレッジグラフの作成方法)
7. [LODチャレンジ向けの説明](#lodチャレンジ2022向けの説明)

## 背景
- 超高齢化社会に伴い，日常生活に潜む安全上・健康上の問題の予測，分析の需要が増加
- データ収集の多くは物理機材や被験者を要し，コストがかかる上に条件変更が難しく，ライセンス上制限が厳しい
- 収集データ内に意味的な関係が不足しているため，意味やコンテキストを考慮した分析が難しい

## 提案データセット
- 仮想空間内で日常生活行動をシミュレーションした動画データ
- 動画の内容をナレッジグラフ化したデータ（"誰"がどんな"物"にどんな"行動"をしてその結果"物の状態"や"位置関係"がどうなったか）
- 上記をオープンデータとして公開

## データセットの構成
- [動画](./Movie/)
  - mp4形式
  - 30種類の行動シナリオ
  - 1種類につきキャラクター後方視点（ファイル名末尾0），室内カメラ視点（ファイル名末尾1）があり，合計60個の動画
- [ナレッジグラフ](./RDF/)
  - RDF形式
  - 動画に対応する30個のナレッジグラフ
  - スキーマは[後述](#ナレッジグラフの説明)
- [台本データ](./Program/)
  - txt形式
  - 動画とナレッジグラフを生成するために[VirtualHome2KG](https://github.com/aistairc/VirtualHome2KG)に与えたデータ
  - 行動のタイトルと簡単な文章説明を含む


## ナレッジグラフの説明

### オントロジーの仕様書
全クラス・インスタンス・プロパティの説明は下記の仕様書を御覧ください。  
[https://aistairc.github.io/VirtualHome2KG/vh2kg_ontology.html](https://aistairc.github.io/VirtualHome2KG/vh2kg_ontology.html)  
以下で代表的なクラス・プロパティを説明します。

### スキーマ図
<img src="https://github.com/aistairc/VirtualHome2KG/raw/main/ontology/image/class_diagram.png" alt="schema">


<details>
<summary>接頭辞</summary>
<table>
    <tr>
        <td>Prefix</td>
        <td>URI</td>
    </tr>
    <tr>
        <td>:</td>
        <td>http://example.org/virtualhome2kg/ontology/</td>
    </tr>
    <tr>
        <td>ho:</td>
        <td>http://www.owl-ontologies.com/VirtualHome.owl#</td>
    </tr>
    <tr>
        <td>time:</td>
        <td>http://www.w3.org/2006/time#</td>
    </tr>
    <tr>
        <td>x3do</td>
        <td>https://www.web3d.org/specifications/X3dOntology4.0#</td>
    </tr>
</table>
</details>

<details>
<summary>代表的なクラス</summary>
<table>
    <tr>
        <td>QName</td>
        <td>Description</td>
    </tr>
    <tr>
        <td>ho:Activity</td>
        <td>家庭での人間の日常活動。このクラスは<a href="https://github.com/valexande/HomeOntology" target="_blank">HomeOntology</a>から再利用されている。</td>
    </tr>
    <tr>
        <td>:Event</td>
        <td>アクティビティを構成する細かなイベント。</td>
    </tr>
    <tr>
        <td>:Action</td>
        <td>イベント内で行われる人間の動作（アクション）。</td>
    </tr>
    <tr>
        <td>:Object</td>
        <td>食べ物、家具、電化製品、消耗品、生活用品など、家庭内にある様々なオブジェクト。</td>
    </tr>
    <tr>
        <td>:Situation</td>
        <td>特定の瞬間における家庭内の状況。その瞬間における家庭内のすべてのオブジェクトの状態（State）インスタンスは、このクラスのインスタンスの一部分(part)となる。</td>
    </tr>
    <tr>
        <td>:State</td>
        <td>特定の瞬間における、特定の物体の状態。イベントの前後で状態が変化する場合にのみ新たにインスタンスが作成される。</td>
    </tr>
    <tr>
        <td>:StateType</td>
        <td>オブジェクトの状態の種類. このクラスのインスタンスは、VirtualHomeの<a href="https://github.com/xavierpuigf/virtualhome/tree/master/src/virtualhome/simulation#object-states" target="_blank">object states</a>に基づいている。</td>
    </tr>
    <tr>
        <td>:Attribute</td>
        <td>オブジェクトの属性。</td>
    </tr>
    <tr>
        <td>:Shape</td>
        <td>オブジェクトの形状と位置を表すクラス。サイズと座標を含む3Dバウンディングボックスの値を持つ。このクラスは<a href="https://www.web3d.org/x3d/content/semantics/semantics.html" target="_blank">X3D ontology</a>から再利用されている。</td>
    </tr>
    <tr>
        <td>time:Duration</td>
        <td>動作の実行時間（秒数）。 このクラスは<a href="https://www.w3.org/TR/owl-time/#time:Duration">Time Ontology</a>から再利用されている。</td>
    </tr>
</table>
</details>

<details>
<summary>代表的なプロパティ</summary>
<table>
    <tr>
        <td>QName</td>
        <td>Domains</td>
        <td>Ranges</td>
        <td>Description</td>
    </tr>
    <tr>
        <td>:activty</td>
        <td>:Character</td>
        <td>:Activity</td>
        <td>キャラクター（エージェント）とアクティビティを関連付ける。</td>
    </tr>
    <tr>
        <td>:action</td>
        <td>:Event</td>
        <td>:Action</td>
        <td>イベントとアクション(動作)を関連付ける。アクティビティはアクションのシーケンスで構成される。</td>
    </tr>
    <tr>
        <td>:eventNumber</td>
        <td>:Event</td>
        <td>xsd:int</td>
        <td>アクティビティにおけるイベントの順序を示す。</td>
    </tr>
    <tr>
        <td>:situationBeforeEvent</td>
        <td>:Event</td>
        <td>:Situation</td>
        <td>あるイベントをある状況に関連付ける。何らかのイベントが実行される前の家庭内の状況。</td>
    </tr>
    <tr>
        <td>:situationAfterEvent</td>
        <td>:Event</td>
        <td>:Situation</td>
        <td>あるイベントをある状況に関連付ける。何らかのイベントが実行された後の家庭内の状況。</td>
    </tr>
    <tr>
        <td>:mainObject</td>
        <td>:Event</td>
        <td>:Object</td>
        <td>ho:objectのサブプロパティ。イベントをメインオブジェクトに関連付ける。イベントにおける動作対象のオブジェクトを表す。「object_Xをobject_Yにactionする」のような場合、object_Xを指定する場合にこのプロパティを使う。</td>
    </tr>
    <tr>
        <td>:targetObject</td>
        <td>:Event</td>
        <td>:Object</td>
        <td>ho:objectのサブプロパティ。イベントをターゲットオブジェクトに関連付ける。イベントにおける動作対象のオブジェクトを表す。「object_Xをobject_Yにactionする」のような場合、object_Yを指定する場合にこのプロパティを使う。</td>
    </tr>
    <tr>
        <td>time:hasDuration</td>
        <td>:Event</td>
        <td>time:Duration</td>
        <td>イベントとその実行時間を関連付ける。</td>
    </tr>
    <tr>
        <td>:isStateOf</td>
        <td>:State</td>
        <td>:Object</td>
        <td>オブジェクトとその状態を関連付ける。</td>
    </tr>
    <tr>
        <td>:state</td>
        <td>:State</td>
        <td>:StateType</td>
        <td>状態をその値に関連付ける。</td>
    </tr>
    <tr>
        <td>:affords</td>
        <td>:Object</td>
        <td>:Action</td>
        <td>オブジェクトとアクションを関連付ける。オブジェクトのアフォーダンスを意味する。</td>
    </tr>
    <tr>
        <td>:attribute</td>
        <td>:Object</td>
        <td>:Attribute</td>
        <td>オブジェクトに属性を関連付ける。</td>
    </tr>
    <tr>
        <td>:partOf</td>
        <td>:State</td>
        <td>:Situation</td>
        <td>オブジェクトの状態(State)が、どの瞬間の家庭内の状況(Situtation)のものであるかを表す。</td>
    </tr>
    <tr>
        <td>:bbox</td>
        <td>:State</td>
        <td>:Shape</td>
        <td>ある時点でのオブジェクトの状態のリソースと形状リソースを関連付ける。</td>
    </tr>
    <tr>
        <td>:nextActivity</td>
        <td>:Activity</td>
        <td>:Activity</td>
        <td>アクティビティ間の関係を表す。次のアクティビティ。</td>
    </tr>
    <tr>
        <td>:nextEvent</td>
        <td>:Event</td>
        <td>:Event</td>
        <td>イベント間の関係を表す。次のイベント。</td>
    </tr>
    <tr>
        <td>:nextSituation</td>
        <td>:Situation</td>
        <td>:Situation</td>
        <td>状況間の関係を表す。次の状況。</td>
    </tr>
    <tr>
        <td>:nextState</td>
        <td>:State</td>
        <td>:State</td>
        <td>オブジェクトの状態間の関係を表す。オブジェクトの次の状態。</td>
    </tr>
    <tr>
        <td>:between</td>
        <td>:Shape</td>
        <td>:Shape</td>
        <td>主にドアオブジェクトに適応される。キッチンとリビングの間にドアがある場合、このプロパティはドアとリビング、ドアとキッチンの関係に使用される。詳細はVirtualHomeの<a href="https://github.com/xavierpuigf/virtualhome/tree/master/src/virtualhome/simulation#relations" target="_blank">relations</a>をご覧ください。</td>
    </tr>
    <tr>
        <td>:close</td>
        <td>:Shape</td>
        <td>:Shape</td>
        <td>オブジェクト間の距離が1.5m以内であることを意味する。詳細はVirtualHomeの<a href="https://github.com/xavierpuigf/virtualhome/tree/master/src/virtualhome/simulation#relations" target="_blank">relations</a>をご覧ください。</td>
    </tr>
    <tr>
        <td>:facing</td>
        <td>:Shape</td>
        <td>:Shape</td>
        <td>オブジェクト1からオブジェクト2が見えることを意味する。オブジェクトの中心間の距離が5m以内。詳細はVirtualHomeの<a href="https://github.com/xavierpuigf/virtualhome/tree/master/src/virtualhome/simulation#relations" target="_blank">relations</a>をご覧ください。</td>
    </tr>
    <tr>
        <td>:holds_lh</td>
        <td>:Shape</td>
        <td>:Shape</td>
        <td>左手でオブジェクトを持っていることを意味する。したがって主語はCharacterに関するShapeである。詳細はVirtualHomeの<a href="https://github.com/xavierpuigf/virtualhome/tree/master/src/virtualhome/simulation#relations" target="_blank">relations</a>をご覧ください。</td>
    </tr>
    <tr>
        <td>:holds_rh</td>
        <td>:Shape</td>
        <td>:Shape</td>
        <td>右手でオブジェクトを持っていることを意味する。したがって主語はCharacterに関するShapeである。詳細はVirtualHomeの<a href="https://github.com/xavierpuigf/virtualhome/tree/master/src/virtualhome/simulation#relations" target="_blank">relations</a>をご覧ください。</td>
    </tr>
    <tr>
        <td>:inside</td>
        <td>:Shape</td>
        <td>:Shape</td>
        <td>オブジェクト1がオブジェクト2の中に位置していることを意味する。詳細はVirtualHomeの<a href="https://github.com/xavierpuigf/virtualhome/tree/master/src/virtualhome/simulation#relations" target="_blank">relations</a>をご覧ください。</td>
    </tr>
    <tr>
        <td>:on</td>
        <td>:Shape</td>
        <td>:Shape</td>
        <td>オブジェクト1がオブジェクト2の上に位置していることを意味する。</td>
    </tr>
</table>
</details>

### 具体的なナレッジグラフの説明
<img src="./asset/Slide3.png" alt="kgの例 (listen to music)">

## ナレッジグラフの使用方法
ナレッジグラフはRDF形式のデータで提供しているため，トリプルストアに格納することで，クエリ言語SPARQLを使用して様々な検索が可能です．また，[SPARQLエンドポイント](#sparqlエンドポイント)を提供していますので，そちらから直接ご利用いただけます．

参考資料:
- 【トリプルストアについての参考資料】[トリプルストアの導入](https://www.slideshare.net/KnowledgeGraph/lod-250078657)  （12ページから）
- 【SPARQLについての参考資料】[Wikidataを例としたSPARQLクエリの例](https://www.slideshare.net/KnowledgeGraph/linked-open-data2020-sparqlsparql)（16ページから）

  
### SPARQLエンドポイント
本データセットを格納したSPARQLエンドポイントを提供しています。  
[http://kgrc4si.ml:7200/sparql](http://kgrc4si.ml:7200/sparql)  
リポジトリは「KGRC4SIv0」を選択してください。（2022/10/15時点）  
トリプルストアとしてOntotext GraphDBを使用しています．基本的な使用方法は[こちらの動画](https://drive.google.com/file/d/19YKSsUalvVSGinYtCwi2R7zHIp3W0EBU/view)を御覧ください。

### SPARQLクエリ例

- [アクティビティの一覧を取得する](#アクティビティの一覧を取得する)
- [「インターネットをブラウズする」というアクティビティ中のイベントとアクションを取得する](#インターネットをブラウズするというアクティビティ中のイベントとアクションを取得する)
- [よく掴まれているオブジェクト](#よく掴まれているオブジェクト)
- [インタラクションしているオブジェクトのタイプ一覧](#インタラクションしているオブジェクトのタイプ一覧)
- [オブジェクトの高さ情報を追加する](#オブジェクトの高さ情報を追加する)


#### アクティビティの一覧を取得する
```sparql
PREFIX ex: <http://example.org/virtualhome2kg/instance/>
PREFIX : <http://example.org/virtualhome2kg/ontology/>
select DISTINCT * where {
    ?activity :virtualHome ex:scene1 .
}
```
[実行結果](http://kgrc4si.ml:7200/sparql?name=&infer=true&sameAs=false&query=PREFIX%20ex%3A%20%3Chttp%3A%2F%2Fexample.org%2Fvirtualhome2kg%2Finstance%2F%3E%0APREFIX%20%3A%20%3Chttp%3A%2F%2Fexample.org%2Fvirtualhome2kg%2Fontology%2F%3E%0Aselect%20DISTINCT%20*%20where%20%7B%0A%20%20%20%20%3Factivity%20%3AvirtualHome%20ex%3Ascene1%20.%0A%7D)

#### 「インターネットをブラウズする」というアクティビティ中のイベントとアクションを取得する
```sparql
PREFIX ex: <http://example.org/virtualhome2kg/instance/>
PREFIX : <http://example.org/virtualhome2kg/ontology/>
select DISTINCT * where {
    ex:browse_internet_scene1 :hasEvent ?event .
    ?event :action ?action .
}
```
[実行結果](http://kgrc4si.ml:7200/sparql?name=&infer=true&sameAs=false&query=PREFIX%20ex%3A%20%3Chttp%3A%2F%2Fexample.org%2Fvirtualhome2kg%2Finstance%2F%3E%0APREFIX%20%3A%20%3Chttp%3A%2F%2Fexample.org%2Fvirtualhome2kg%2Fontology%2F%3E%0Aselect%20DISTINCT%20*%20where%20%7B%0A%20%20%20%20ex%3Abrowse_internet_scene1%20%3AhasEvent%20%3Fevent%20.%0A%20%20%20%20%3Fevent%20%3Aaction%20%3Faction%20.%0A%7D)

#### インタラクションしているオブジェクトのタイプ一覧
```sparql
PREFIX : <http://example.org/virtualhome2kg/ontology/>
select distinct ?objectType where { 
    ?event (:mainObject|:targetObject) ?object .
    ?object a ?objectType .
}
```
[実行結果](http://kgrc4si.ml:7200/sparql?name=&infer=true&sameAs=false&query=PREFIX%20%3A%20%3Chttp%3A%2F%2Fexample.org%2Fvirtualhome2kg%2Fontology%2F%3E%0Aselect%20distinct%20%3FobjectType%20where%20%7B%20%0A%20%20%20%20%3Fevent%20(%3AmainObject%7C%3AtargetObject)%20%3Fobject%20.%0A%20%20%20%20%3Fobject%20a%20%3FobjectType%20.%0A%7D)

#### よく掴まれているオブジェクト
```sparql
PREFIX ho: <http://www.owl-ontologies.com/VirtualHome.owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX : <http://example.org/virtualhome2kg/ontology/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX ac: <http://example.org/virtualhome2kg/ontology/action/>
select ?name (count(?object) AS ?count) where { 
	?objectClass rdfs:subClassOf :Object .
    ?object a ?objectClass ;
            rdfs:label ?label ; 
            dcterms:identifier ?id .
    ?event ho:object ?object .
    ?event :action ac:grab .
    BIND(concat(?label, ?id) AS ?name)
} group by ?object ?name order by desc(count(?object))
```
[実行結果](http://kgrc4si.ml:7200/sparql?name=&infer=true&sameAs=false&query=PREFIX%20ho%3A%20%3Chttp%3A%2F%2Fwww.owl-ontologies.com%2FVirtualHome.owl%23%3E%0APREFIX%20rdfs%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0APREFIX%20%3A%20%3Chttp%3A%2F%2Fexample.org%2Fvirtualhome2kg%2Fontology%2F%3E%0APREFIX%20dcterms%3A%20%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0APREFIX%20ac%3A%20%3Chttp%3A%2F%2Fexample.org%2Fvirtualhome2kg%2Fontology%2Faction%2F%3E%0Aselect%20%3Fname%20(count(%3Fobject)%20AS%20%3Fcount)%20where%20%7B%20%0A%09%3FobjectClass%20rdfs%3AsubClassOf%20%3AObject%20.%0A%20%20%20%20%3Fobject%20a%20%3FobjectClass%20%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20rdfs%3Alabel%20%3Flabel%20%3B%20%0A%20%20%20%20%20%20%20%20%20%20%20%20dcterms%3Aidentifier%20%3Fid%20.%0A%20%20%20%20%3Fevent%20ho%3Aobject%20%3Fobject%20.%0A%20%20%20%20%3Fevent%20%3Aaction%20ac%3Agrab%20.%0A%20%20%20%20BIND(concat(%3Flabel%2C%20%3Fid)%20AS%20%3Fname)%0A%7D%20group%20by%20%3Fobject%20%3Fname%20order%20by%20desc(count(%3Fobject)))

#### オブジェクトの高さ情報を追加する
```sparql
PREFIX x3do: <https://www.web3d.org/specifications/X3dOntology4.0#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX : <http://example.org/virtualhome2kg/ontology/>
PREFIX ex: <http://example.org/virtualhome2kg/instance/>
CONSTRUCT {
    ?object :height ?height_node .
    ?height_node rdf:value ?size_y1 ;
           :unit :meter .
} WHERE {
	?state1 :isStateOf ?object ; :bbox ?shape1 .
	?shape1 x3do:bboxSize ?size1 .
	?size1 rdf:rest ?size_y .
    ?size_y rdf:first ?size_y1 .
    BIND(REPLACE(STR(?object), STR(ex:) ,"") AS ?object_name)
    BIND(URI(CONCAT(STR(ex:),"height_", ?object_name)) AS ?height_node)
}
```
[実行結果](http://kgrc4si.ml:7200/sparql?name=&infer=false&sameAs=false&query=PREFIX%20x3do%3A%20%3Chttps%3A%2F%2Fwww.web3d.org%2Fspecifications%2FX3dOntology4.0%23%3E%0APREFIX%20rdf%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0APREFIX%20%3A%20%3Chttp%3A%2F%2Fexample.org%2Fvirtualhome2kg%2Fontology%2F%3E%0APREFIX%20ex%3A%20%3Chttp%3A%2F%2Fexample.org%2Fvirtualhome2kg%2Finstance%2F%3E%0ACONSTRUCT%20%7B%0A%20%20%20%20%3Fobject%20%3Aheight%20%3Fheight_node%20.%0A%20%20%20%20%3Fheight_node%20rdf%3Avalue%20%3Fsize_y1%20%3B%0A%20%20%20%20%20%20%20%20%20%20%20%3Aunit%20%3Ameter%20.%0A%7D%20WHERE%20%7B%0A%09%3Fstate1%20%3AisStateOf%20%3Fobject%20%3B%20%3Abbox%20%3Fshape1%20.%0A%09%3Fshape1%20x3do%3AbboxSize%20%3Fsize1%20.%0A%09%3Fsize1%20rdf%3Arest%20%3Fsize_y%20.%0A%20%20%20%20%3Fsize_y%20rdf%3Afirst%20%3Fsize_y1%20.%0A%20%20%20%20BIND(REPLACE(STR(%3Fobject)%2C%20STR(ex%3A)%20%2C%22%22)%20AS%20%3Fobject_name)%0A%20%20%20%20BIND(URI(CONCAT(STR(ex%3A)%2C%22height_%22%2C%20%3Fobject_name))%20AS%20%3Fheight_node)%0A%7D)

## 同様のナレッジグラフの作成方法
本データセットは我々の提案システム「[VirtualHome2KG](https://github.com/aistairc/VirtualHome2KG)」を使用して作成されています。  
詳細はこちらの資料を御覧ください。

## LODチャレンジ2022向けの説明
- Impact - 影響力
  - 高齢者の家庭内における事故につながる可能性がある，危険な行動や危険な状況を発見し説明する手法の開発を促進します。
  - 動画とナレッジグラフを同時に扱うマルチモーダルAIの開発に資するGround truthデータセットとして発展していくと考えています。
- Creativity - 創造力
  - 日常生活における動作・行動（意味のある動作のまとまり）・モノ・状態・位置関係・アフォーダンスなどを事細かに記録し，各エンティティがURIとして一貫性のある一意なIDを持ち（参照解決は今後の課題），エンティティ同士が相互に関連付けられたデータセットはこれまでになく，既存のシーングラフよりも多くの情報量を持っています．単にデータを変換しただけでなく，既存のオントロジーやオントロジーデザインパターンを再利用しながら新たなスキーマを提案し，検索性能を高める工夫を施しています．
- Usefulness - 有用性
  - 動画の内容をナレッジグラフとして表現することで，SPARQL例に示したとおり柔軟な検索が可能です。様々な視点から日常生活パターンを分析し，安全上・健康上のリスク回避に役立てる手法やツールを開発するための，ベンチマーク用のデータセットとして機能します．
- Accessibility - 機械可読性
  - ナレッジグラフはRDF形式で提供し，可能な限りエンティティをリテラルではなくURI付きリソースとしており，機械可読性は高いと言えます．
- Openness - 開放性
  - CC BY 4.0ライセンスのオープンデータとして公開しています．
  - RDF化されており，各エンティティに一意なURIが付与されていますが，参照解決は今後の課題としています．
- Linkability - つながる可能性
  - 外部データとして[HomeOntology](https://github.com/valexande/HomeOntolog)，[PrimitiveActionOntology](https://github.com/aistairc/PrimitiveActionOntology)，[HomeObjectOntology](https://github.com/aistairc/HomeObjectOntology)，[Time Ontology](https://www.w3.org/TR/owl-time/#time:Duration)，[X3D ontology](https://www.web3d.org/x3d/content/semantics/semantics.html)などを再利用・参考にしています。
  - 現在，本提案データセットを利用して「[ナレッジグラフ推論チャレンジ【実社会版】](https://challenge.knowledge-graph.jp/2022/)」を開催しており，今後このデータセットを利用して様々な研究・開発が生まれることが見込めます。
  - LODチャレンジ2022の別の応募作品で使用されていることを確認しました（ありがとうございます！）
    - s246wv氏，[virtualhome2kg-Admire_paintings.ttlのbboxを描いてみる](https://github.com/s246wv/viz-kgrc-rdf-bbox-x3dom/tree/master/virtualhome2kg-Admire_paintings)
- Sustainability − 持続可能性
  - 現在，本提案データセットを利用して「[ナレッジグラフ推論チャレンジ【実社会版】](https://challenge.knowledge-graph.jp/2022/)」を開催しており，継続してデータセットを追加しています．今年度中にデータが数十件増える予定となっており，その後もデータ増加・クオリティの向上を検討しています．チャレンジ終了後もGithub repositoryで継続して公開します．

## リファレンス
- 江上周作，鵜飼孝典，窪田文也，大野美喜子，北村光司，福田賢一郎: 家庭内の事故予防に向けた合成ナレッジグラフの構築と推論，第56回人工知能学会セマンティックウェブとオントロジー研究会, SIG-SWO-056-14 (2022) [[J-STAGE]](https://www.jstage.jst.go.jp/article/jsaisigtwo/2022/SWO-056/2022_14/_article/-char/ja)
- Egami, S., Nishimura, S., Fukuda, K.: A Framework for Constructing and Augmenting Knowledge Graphs using Virtual Space: Towards Analysis of Daily Activities. Proceedings of the 33rd IEEE International Conference on Tools with Artificial Intelligence. pp.1226-1230 (2021) [[IEEE Xplore]](https://ieeexplore.ieee.org/document/9643400)
- Egami, S., Nishimura, S., Fukuda, K.: VirtualHome2KG: Constructing and Augmenting Knowledge Graphs of Daily Activities Using Virtual Space. Proceedings of the ISWC 2021 Posters, Demos and Industry Tracks: From Novel Ideas to Industrial Practice, co-located with 20th International Semantic Web Conference. CEUR, Vol.2980 (2021) [[pdf]](http://ceur-ws.org/Vol-2980/paper381.pdf)

## ライセンス
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="クリエイティブ・コモンズ・ライセンス" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br /><a xmlns:cc="http://creativecommons.org/ns#" href="https://profile.idease.info/" property="cc:attributionName" rel="cc:attributionURL">江上周作</a>，他 作『<span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Dataset" property="dct:title" rel="dct:type">VirtualHome2KGデータセット―家庭内の日常生活行動のシミュレーション動画とナレッジグラフ―</span>』は<a rel="license" href="http://creativecommons.org/licenses/by/4.0/">クリエイティブ・コモンズ 表示 4.0 国際 ライセンス</a>で提供されています。<br /><a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/aistairc/VirtualHome2KG" rel="dct:source">https://github.com/aistairc/VirtualHome2KG</a>にある作品に基づいている。

## 謝辞
この成果は，国立研究開発法人新エネルギー・産業技術総合開発機構(NEDO)の委託業務(JPNP20006, JPNP180013)の結果得られたものです．