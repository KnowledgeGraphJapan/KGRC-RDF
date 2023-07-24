[![CC BY 4.0][cc-by-shield]][cc-by]  

This repogitory is for for public use of the Open Knowledge Graph for **[the First International Knowledge Graph Reasoning Challenge 2023](https://ikgrc.org/2023/)**.  

## SPARQL endpoint
- http://kg.hozo.jp/fuseki/ikgrc/sparql (for use as API)
- http://knowledge-graph.jp/sparql-ikgrc.html (for querying on the web browser)  

*Sample queries are availabe at [this page](SampleSPARQL.md).  

## Visualization Tool for the KG
- http://knowledge-graph.jp/visualization/


## Grpaph IRI for each Story 
[Note] When you run SPARQL queries, you have to specfy Graph IRIs using **FROM** sentences．
|Story|Graph IRI|
----|----
|The Speckled Band|&lt;http://kgc.knowledge-graph.jp/data/SpeckledBand&gt;|
|The Dancing Men|&lt;http://kgc.knowledge-graph.jp/data/DancingMen&gt;|
|A Case of Identity|&lt;http://kgc.knowledge-graph.jp/data/ACaseOfIdentity&gt;|
|The Devil's Foot|&lt;http://kgc.knowledge-graph.jp/data/DevilsFoot&gt;|
|The Crooked Man|&lt;http://kgc.knowledge-graph.jp/data/CrookedMan&gt;|
|The Abbey Grange|&lt;http://kgc.knowledge-graph.jp/data/AbbeyGrange&gt;|
|Silver Blaze|&lt;http://kgc.knowledge-graph.jp/data/SilverBlaze&gt;|
|The Resident Patient|&lt;http://kgc.knowledge-graph.jp/data/ResidentPatient&gt;|




## License
This data is licensed under [a Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/) by Special Interest Group on Semantic Web and Ontology, the Japanese Society for AI (SIG-SWO, JSAI).

[![CC BY 4.0][cc-by-image]][cc-by]

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg

## History
### 2020/06/09ver.[2020ver.1] Modified:5 stories + Added:2 stories 
- **5 stories** in [2019ver.](https://github.com/KnowledgeGraphJapan/Challenge/tree/master/rdf/2019) were significantly modified in this version.  
- **2 new stories "The Abbey Grange" and "Silver Blaze"** were added as new Open Knowledge Graphs.  

### 2020/12/24ver. [2020ver.2 tentative] Modified:7 stories + Added:1 story  
- **7 stories** in [2020/10/09ver.](https://github.com/KnowledgeGraphJapan/KGRC-RDF/tree/master/2020) were modified.  
- **new stories "The Resident Patient"** was added as a new Open Knowledge Graph.  

### 2021/01/19ver. [2020ver.2] Modified:3 stories  
- **3 stories** in [[2020ver.2 tentative] were modified as follows:  
  - **"The Abbey Grange"**: The incorrect data was replaced with the correct one．
  - **"The Abbey Grange", "Silver Blaze" and "The Resident Patient"**: The following infomation was added.
    (These infomation is already included in other 5 stories.)
    - Connections between scenes
    - Absolute time (kgc:time)
    - Types of objects (Person, Animal, Place, PysicalObject, AbstractTime)  
   
**The 2020ver.2** is the final version for the Third Knowledge Graph Reasoning Challenge 2020. 

### 2022/10/27ver. [ikgrc] Modified:the all 8 stories
  
