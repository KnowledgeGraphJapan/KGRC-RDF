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
        <td>Human daily activity at home. This class is reused from the HomeOntology.</td>
    </tr>
    <tr>
        <td>:Event</td>
        <td>Fine-grained event to compose the activity.</td>
    </tr>
    <tr>
        <td>:Action</td>
        <td>Primitive action performed in an event.</td>
    </tr>
    <tr>
        <td>:Object</td>
        <td>Object in a home such as food, furniture, electronics, consumables, and living thing.</td>
    </tr>
    <tr>
        <td>:Situation</td>
        <td>Situation in a home at a certain time.</td>
    </tr>
    <tr>
        <td>:State</td>
        <td>State of an object at a certain time.</td>
    </tr>
    <tr>
        <td>:StateType</td>
        <td>Type of state. The instances of this class are based on [object states](https://github.com/xavierpuigf/virtualhome/tree/master/simulation#object-states) of VirtualHome.</td>
    </tr>
    <tr>
        <td>:Attribute</td>
        <td>Attribute of an object.</td>
    </tr>
    <tr>
        <td>:Shape</td>
        <td>Object's 3D bounding box, including size and coordinates. This class is reused from the [X3D ontology](https://www.web3d.org/x3d/content/semantics/semantics.html).</td>
    </tr>
    <tr>
        <td>time:Duration</td>
        <td>Duration of an execution of an action. This class is reused from the [Time Ontology](https://www.w3.org/TR/owl-time/#time:Duration).</td>
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
        <td>Associates a character (agent) to activities.</td>
    </tr>
    <tr>
        <td>:action</td>
        <td>:Activity</td>
        <td>:Action</td>
        <td>Associates an activity to actions. The activity is composed of an action sequence.</td>
    </tr>
    <tr>
        <td>:actionNumber</td>
        <td>:Action</td>
        <td>xsd:int</td>
        <td>Indicates the order of the action in the activity.</td>
    </tr>
    <tr>
        <td>:situationBeforeEvent</td>
        <td></td>
        <td>:Situation</td>
        <td>Subproperty of :relatedSituation. Associates an event to a situation. Environmental situation before executing some action.</td>
    </tr>
    <tr>
        <td>:situationAfterEvent</td>
        <td></td>
        <td>:Situation</td>
        <td>Subproperty of :relatedSituation. Associates an event to a situation. Environmental situation after executing some action.</td>
    </tr>
    <tr>
        <td>ho:object</td>
        <td>:Action</td>
        <td>:Object</td>
        <td>Associates an action to a target object. This property is reused and modified from the HomeOntology.</td>
    </tr>
    <tr>
        <td>time:hasDuration</td>
        <td>:Action</td>
        <td>time:Duration</td>
        <td>Associates an action to its execution duration.</td>
    </tr>
    <tr>
        <td>:isStateOf</td>
        <td>:State</td>
        <td>:Object</td>
        <td>Associates an object to its state.</td>
    </tr>
    <tr>
        <td>:state</td>
        <td>:State</td>
        <td>:StateType</td>
        <td>Associates a state to its values.</td>
    </tr>
    <tr>
        <td>:affords</td>
        <td>:Object</td>
        <td>:Action</td>
        <td>Associates an object to actions. This means affordance.</td>
    </tr>
    <tr>
        <td>:attribute</td>
        <td>:State</td>
        <td>:Attribute</td>
        <td>Associates a state to attributes of an object.</td>
    </tr>
    <tr>
        <td>:partOf</td>
        <td>:State</td>
        <td>:Situation</td>
        <td>In this ontology, the :partOf property is used for associating a state to a situation.</td>
    </tr>
    <tr>
        <td>:bbox</td>
        <td>:State</td>
        <td>:Shape</td>
        <td>Associates a state to a 3D bounding box of an object.</td>
    </tr>
    <tr>
        <td>:nextActivity</td>
        <td>:Activity</td>
        <td>:Activity</td>
        <td>Subproperty of :relatedActivity. Associates an activity to the next activity. This property is usually used for KG that is augmented by our method.</td>
    </tr>
    <tr>
        <td>:nextAction</td>
        <td>:Action</td>
        <td>:Action</td>
        <td>Subproperty of :relatedAction. Associates an action to the next action.</td>
    </tr>
    <tr>
        <td>:nextSituation</td>
        <td>:Situation</td>
        <td>:Situation</td>
        <td>Subproperty of :relatedSituation. Associates a situation to the next situation.</td>
    </tr>
    <tr>
        <td>:nextState</td>
        <td>:State</td>
        <td>:State</td>
        <td>Subproperty of :relatedState. Associates a state to the next state.</td>
    </tr>
    <tr>
        <td>:between</td>
        <td>:Shape</td>
        <td>:Shape</td>
        <td>Subproperty of :relatedShape. Please see [detailed description](https://github.com/xavierpuigf/virtualhome/tree/master/simulation#relations). This property is used for door objects. If a door is between a kitchen and a living room, this property associates the door to the living room and associates the door to the kitchen.</td>
    </tr>
    <tr>
        <td>:close</td>
        <td>:Shape</td>
        <td>:Shape</td>
        <td>Subproperty of :relatedShape. Please see [detailed description](https://github.com/xavierpuigf/virtualhome/tree/master/simulation#relations). Triple &lt;object1, close, object2&gt; denotes that the distance between center of object1 (object2) to the bounding box of object2 (object1) is &lt; 1.5 units (~meters).</td>
    </tr>
    <tr>
        <td>:facing</td>
        <td>:Shape</td>
        <td>:Shape</td>
        <td>Subproperty of :relatedShape. Please see [detailed description](https://github.com/xavierpuigf/virtualhome/tree/master/simulation#relations). Triple &lt;object1, facing, object2&gt; denotes that object2 is lookable, is visible from object1, and the distance between the centers is &lt; 5 units (~meters).</td>
    </tr>
    <tr>
        <td>:holds_lh</td>
        <td>:Shape</td>
        <td>:Shape</td>
        <td>Subproperty of :relatedShape. Please see [detailed description](https://github.com/xavierpuigf/virtualhome/tree/master/simulation#relations). Relation for left hand.</td>
    </tr>
    <tr>
        <td>:holds_rh</td>
        <td>:Shape</td>
        <td>:Shape</td>
        <td>Subproperty of :relatedShape. Please see [detailed description](https://github.com/xavierpuigf/virtualhome/tree/master/simulation#relations). Relation for left hand.</td>
    </tr>
    <tr>
        <td>:inside</td>
        <td>:Shape</td>
        <td>:Shape</td>
        <td>Subproperty of :relatedShape. Triple &lt;object1, inside, object2&gt; denotes that object1 is placed inside of object2.</td>
    </tr>
    <tr>
        <td>:on</td>
        <td>:Shape</td>
        <td>:Shape</td>
        <td>Subproperty of :relatedShape. Triple &lt;object1, on, object2&gt; denotes that object1 is placed on object2.</td>
    </tr>
</table>
</details>

