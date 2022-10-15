# 家庭内の日常生活行動の合成動画および合成ナレッジグラフ

<table>
<tr>
<td><img src="./asset/put_food_in_fridge1.gif" width="290" alt="video"></td>
<td><img src="./asset/put_food_in_fridge1_kg.png" width="300" alt="kg"></td>
</tr>
</table>

## 簡単に言うと
- 家庭内日常生活を仮想空間でシミュレーションした動画と，その内容を表すナレッジグラフのセット

## 目次
1. [背景](#背景)
2. [提案データセット](#提案データセット)
3. [データセットの構成](#データセットの構成)
4. [ナレッジグラフの説明](#ナレッジグラフの説明)
5. [ナレッジグラフの使用方法](#ナレッジグラフの使用方法)
6. [同様のナレッジグラフの作成方法](#同様のナレッジグラフの作成方法)

## 背景
- 超高齢化社会に伴い，日常生活に潜む安全上・健康上の問題の予測，分析の需要が増加
- データ収集の多くは物理機材や被験者を要し，コストがかかる上に条件変更が難しい
- 収集データ内に意味的な関係が不足しているため，意味やコンテキストを考慮した分析が難しい

## 提案データセット
- 仮想空間内で日常生活行動をシミュレーションした動画データ
- 動画の内容をナレッジグラフ化したデータ（"誰"がどんな"物"にどんな"行動"をしてその結果"物の状態"や"位置関係"がどうなったか）

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

### スキーマ図
<img src="https://github.com/aistairc/VirtualHome2KG/raw/main/ontology/image/class_diagram.png" alt="schema" width="80%">


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
<summary>プロパティ</summary>
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

### 仕様書
全クラス・インスタンス・プロパティの説明は下記の仕様書を御覧ください。  
[https://aistairc.github.io/VirtualHome2KG/vh2kg_ontology.html](https://aistairc.github.io/VirtualHome2KG/vh2kg_ontology.html)

### 具体的なナレッジグラフの説明
<img src="./asset/Slide3.png" alt="kgの例 (listen to music)">

## ナレッジグラフの使用方法
ナレッジグラフはRDF形式のデータで提供しているため，トリプルストアに格納することで，クエリ言語SPARQLを使用して様々な検索が可能です．

参考資料:
- 【トリプルストアについての参考資料】[トリプルストアの導入](https://www.slideshare.net/KnowledgeGraph/lod-250078657)  （12ページから）
- 【SPARQLについての参考資料】[Wikidataを例としたSPARQLクエリの例](https://www.slideshare.net/KnowledgeGraph/linked-open-data2020-sparqlsparql)（16ページから）

  
### SPARQLエンドポイント
本データセットを格納したSPARQLエンドポイントを提供しています。
