[HOME](index.md)
[FULL REPORT](another-page.md)

<h3 style="color:blue; font-size: 2em;">CONCLUSION AND RESULTS</h3>

To sum up we can remark that LLMs have proven to be powerful instruments, even though they must be properly instructed and sometimes even corrected in order to obtain the required information. Furthermore, the fact that several Classes and Properties existing in the ArCo Ontology are not actually used makes it difficult to understand how to use them and to create triples.

These are the triples we propose to enrich the ArCo knowledge graph:

<a name="mm-anchor"></a>
<h3 style="color:blue ;">Andrea Mantegna</h3>

<b>1.Triple:</b><br>
<a href="https://dati.beniculturali.it/lodview-arco/resource/HistoricOrArtisticProperty/0300180068.html">https://dati.beniculturali.it/lodview-arco/resource/HistoricOrArtisticProperty/0300180068.html</a> --> Subject <br>
<a href= "https://w3id.org/arco/ontology/context-description/hasRelatedWork">a-cd:hasRelatedWork</a> --> Predicate <br>
<a href="https://w3id.org/arco/resource/PreparatoryWork/0300182725-dipinto">https://w3id.org/arco/resource/PreparatoryWork/0300182725-dipinto</a> --> Object <br>

<b>2.Triple:</b> <br>
<a href= "https://w3id.org/arco/resource/PreparatoryWork/0300182725-dipinto">https://w3id.org/arco/resource/PreparatoryWork/0300182725-dipinto</a> --> Subject <br> 
<a href= "https://w3id.org/arco/ontology/context-description/isWorkRelatedTo">a-cd:isWorkRelatedTo</a> --> Predicate <br>
<a href="https://w3id.org/arco/resource/HistoricOrArtisticProperty/0300180068">https://w3id.org/arco/resource/HistoricOrArtisticProperty/0300180068</a> --> Object <br>

<a name="mm-anchor"></a>
<h3 style="color:blue ;">Cristo morto</h3>

<b>1.Triple:</b> <br>
<a href= "https://w3id.org/arco/resource/HistoricOrArtisticProperty/0300180068">https://w3id.org/arco/resource/HistoricOrArtisticProperty/0300180068</a> --> Subject <br>
<a href= "https://dati.beniculturali.it/lodview-arco-onto/ontology/context-description/hasDating.html">a-cd:hasDating</a> --> Predicate <br>
https://w3id.org/arco/resource/AlternativeDating/0300180068 --> Object <br>

<b>2.Triple:</b> <br>
https://w3id.org/arco/resource/AlternativeDating/0300180068 --> Subject <br>
<a href= "https://w3id.org/arco/ontology/context-description/hasAlternativeDatingType">a-cd:hasAlternativeDatingType</a> --> Predicate <br>
<a href= "https://w3id.org/arco/ontology/context-description/DifferentDating">a-cd:differentDating</a> --> Object <br>

<b>3.Triple:</b> <br>
<a href= "https://w3id.org/arco/resource/AlternativeDating/0300180068">https://w3id.org/arco/resource/AlternativeDating/0300180068</a> --> Subject <br>
<a href= "https://w3id.org/arco/ontology/context-description/hasDatingEvent">a-cd:hasDatingEvent</a> --> Predicate <br>
https://w3id.org/arco/resource/Event/0300180068-creation-2 --> Object <br>

<b>4.Triple:</b> <br>
<a href= "https://w3id.org/arco/resource/Event/0300180068-creation-2">https://w3id.org/arco/resource/Event/0300180068-creation-2</a> --> Subject <br>
<a href="https://w3id.org/arco/ontology/context-description/specificTime">a-cd:specificTime</a> --> Predicate <br>
<a href= "https://w3id.org/arco/resource/TimeInterval/ca-1480-ca-1483">https://w3id.org/arco/resource/TimeInterval/ca-1480-ca-1483</a> --> Object <br>

<b>5.Triple:</b> <br>
<a href= "https://w3id.org/arco/resource/CulturalEvent/a5cc0077c01891152d8d380f41ebed0e">https://w3id.org/arco/resource/CulturalEvent/a5cc0077c01891152d8d380f41ebed0e</a> --> Subject <br>
<a href= "http://dati.beniculturali.it/cis/isHostedBySite">cis:isHostedBySite</a> --> Predicate <br>
<a href= "https://w3id.org/arco/resource/Lombardia/Site/88bbeb320f82f33c71368ac984b74f06">https://w3id.org/arco/resource/Lombardia/Site/88bbeb320f82f33c71368ac984b74f06</a> --> Object

<a name="mm-anchor"></a>
<h3 style="color:blue ;">San Giorgio e il drago</h3>

<b>1.Triple:</b> <br>
<a href= "https://w3id.org/arco/resource/HistoricOrArtisticProperty/0500402340">https://w3id.org/arco/resource/HistoricOrArtisticProperty/0500402340</a> --> Subject <br>
<a href= "https://dati.beniculturali.it/lodview-arco/ontology/denotative-description/hasMaterialOrTechnique.html">a-dd:hasMaterialOrTechnique</a> --> Predicate <br>
<a href= "https://w3id.org/arco/resource/TechnicalCharacteristic/pittura-a-tempera">https://w3id.org/arco/resource/TechnicalCharacteristic/pittura-a-tempera</a> --> Object <br>

<b>2.Triple:</b> <br>
<a href= "https://w3id.org/arco/resource/HistoricOrArtisticProperty/0500402340">https://w3id.org/arco/resource/HistoricOrArtisticProperty/0500402340</a> --> Subject <br>
<a href= "https://dati.beniculturali.it/lodview-arco/ontology/denotative-description/hasMaterialOrTechnique.html">a-dd:hasMaterialOrTechnique</a> --> Predicate <br>
<a href= "https://w3id.org/arco/resource/TechnicalCharacteristic/tavola-pittura-a-tempera">https://w3id.org/arco/resource/TechnicalCharacteristic/tavola-pittura-a-tempera</a> --> Object <br>

[HOME](index.md)
[FULL REPORT](another-page.md)
