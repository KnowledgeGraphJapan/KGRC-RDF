 [[Japanese](README_ja.md)]
 
 # Dataset for Knowledge Graph Reasoning Challenge for Social Issue
<table width="100%">
<tr>
<td width="49%"><img src="./asset/put_food_in_fridge1.gif" alt="video"></td>
<td width="51%"><img src="./asset/put_food_in_fridge1_kg.png" alt="kg"></td>
</tr>
</table>

## Table of Contents
1. [Provided_Dataset](#Provided_Dataset)
2. [Dataset_Composition](#Dataset_Composition)
3. [Explanation of Knowledge Graphs](#Explanation_of_Knowledge_Graphs)
4. [How to Use Knowledge Graphs](#How_to_Use_Knowledge_Graphs)
5. [Creating Similar Knowledge Graphs](#Creating_Similar_Knowledge_Graphs)

## Provided_Dataset
- Video data that simulates daily life actions in a virtual space
- Data that turns the content of the videos into knowledge graphs ("who" did what "action" with what "object" and the resulting "state" or "position" of the object)
- This data is open to the public as open data.

## Dataset_Composition
- [Videos](./Movie)
  - mp4 format
  - 204 action scenarios (updated: 2023/02/21)
  - For each scenario, there is a character rear view (file name ending in 0), an indoor camera switching view (file name ending in 1), and a fixed camera view placed in each corner of the room (file name ending in 2-5). Also, for each action scenario, data was generated for a minimum of 1 to a maximum of 7 patterns with different room layouts (scenes). A total of 1,224 videos (updated: 2023/02/21)
  - Videos with slowly moving characters simulate the movements of elderly people.

## Knowledge Graphs
- [RDF format](./RDF)
  - 204 knowledge graphs corresponding to the videos (updated: 2023/02/21)
  - Includes schema and location supplement information
  - The schema is described below
  - [SPARQL endpoints](http://kgrc4si.ml:7200/sparql) and [query examples](https://github.com/KnowledgeGraphJapan/KGRC-RDF/tree/kgrc4si#%E3%83%8A%E3%83%AC%E3%83%83%E3%82%B8%E3%82%B0%E3%83%A9%E3%83%95%E3%81%AE%E4%BD%BF%E7%94%A8%E6%96%B9%E6%B3%95) are available
- [Script Data](./Program)
  - txt format
  - Data provided to VirtualHome2KG to generate videos and knowledge graphs
  - Includes the action title and a brief description in text format.
