
<div class="topnav">
  <a class="active" href="https://kevinits-site.github.io">Home</a>
  <a class="active" href="https://kevinits-site.github.io/triples.html">Results</a>
</div>


<h3 style="color:blue; font-size: 2em;">CONTENT</h3>

1. [Introduction](#mm-anchor)

2. [Andrea Mantegna](#target-section)
   
3. [Cristo Morto, Andrea Mantegna](#custom-anchor)
   
4. [San Giorgio e il drago, Andrea Mantegna](#c-anchor)
   <div style="margin-top: 60px;"></div> 

<a name="mm-anchor"></a>
<h4 style="color:blue; font-weight: bold;">1. Introduction</h4>

The goal of our project was to explore the artworks of the Italian Renaissance painter Andrea Mantegna within ArCo’s knowledge graph and discover potential ways to enrich the KG through the creation of new RDF triples. To do this, we decided to conduct a general analysis of the artist’s paintings, trying to find out which ones presented missing or incomplete information. 

<a name="target-section"></a>
<h4 style="color:blue; font-weight: bold">2. Andrea Mantegna</h4>

<div style="text-align: center;">
  <img src="![mantegna](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/ec53a451-a589-471e-a4bb-9778059757ed)">
</div>

Exploring ArCo

Our first step is looking for all the cultural properties authored by Andrea Mantegna. However, since we don’t have an IRI for the author yet, we build a query for all the strings whose value contains the words “Andrea Mantegna”:

<p style="background-color: Azure; padding: 5px;">
  PREFIX arco: <https://w3id.org/arco/ontology/arco/> <br>
  PREFIX a-cd: <https://w3id.org/arco/ontology/context-description/> <br>
  PREFIX agent: <https://w3id.org/arco/resource/Agent/> <br>

  SELECT DISTINCT ?culturalProperty ?title <br>
  WHERE { <br>
    ?culturalProperty a-cd:hasAuthor ?author ; <br>
    rdfs:label ?title . <br>
    ?author rdfs:label ?authorName <br>
    FILTER(?authorName = "Andrea Mantegna") <br>
  } <br>
</p>

The first thing we notice from the results of our query is that most of the entities retrieved are of class “PreparatoryWork”. Moreover, none of these cultural properties appears to be one of Mantegna’s famous artworks, which means that these works are either not present or they exist but are associated to an alternative agent whose name is slightly different:

![bild 1](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/00977159-d961-4583-8fa9-cb6a3c210769)

Although we are not satisfied with the result, we are keeping this first, preliminary IRI retrieved for the painter: <br>
<https://w3id.org/arco/resource/Agent/12f2edbd230290b2abfb6c867ecef84b> (prel) <br>
At this point, we try to modify the target of our query by making it more specific. This is why we decide to build a query in order to search for one specific famous painting by Mantegna, the "Cristo Morto". We include the full title of the painting in our query , knowing that, since this subject is very popular in the history of art, it could give us too many results. 

<p style="background-color: Azure; padding: 5px;">
PREFIX arco: <https://w3id.org/arco/ontology/arco/> <br>
PREFIX a-cd: <https://w3id.org/arco/ontology/context-description/> <br>
PREFIX agent: <https://w3id.org/arco/resource/Agent/> <br>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> <br>
SELECT DISTINCT ?cp <br>
WHERE { <br>
?cp a arco:HistoricOrArtisticProperty ; <br>
rdfs:label ?l . <br>
FILTER(REGEX(?l, "cristo morto nel sepolcro e tre dolenti", "i")) <br>
} <br>
</p>
  
This query successfully returns us two results:

![bild 2](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/2bc78b9b-7303-4d6a-b691-6572535e49d9)

After querying for the properties and values associated with both entities in the ArCo dataset, and checking the property cd:hasAuthor, we are able to identify two other IRIs for the author Andrea Mantegna.

<p style="background-color: Azure; padding: 5px;">
PREFIX arco: <https://w3id.org/arco/ontology/arco/> <br>
SELECT ?property ?value <br>
WHERE { <br>
  <https://w3id.org/arco/resource/HistoricOrArtisticProperty/0300180068> ?property ?value . <br>
} <br>
</p>

<p style="background-color: Azure; padding: 5px;">
PREFIX arco: <https://w3id.org/arco/ontology/arco/> <br>
SELECT ?property ?value <br>
WHERE { <br>
<https://w3id.org/arco/resource/Lombardia/HistoricOrArtisticProperty/RL480-00068_R03> ?property ?value . <br>
} <br>
</p>

FIRST IRI: (b) <https://w3id.org/arco/resource/Agent/f006a78cf246d5b7d73539da8eac78e3> <br>
SECOND IRI: (c) <https://w3id.org/arco/resource/Lombardia/Agent/5fd98076b40717d5f8162f1580228220> 

At first glance, we notice that the main difference between the two lies in the fact that the second IRI includes 'Lombardia’. Therefore, our suspicion is that the second IRI places the Agent Mantegna specifically within the context of the region Lombardy. This could imply that within the ArCo dataset, there is specific attributes related to Mantegna that pertain to Lombardy, such as artworks located in that region. To confirm this hypothesis, we compare the number of cultural properties authored by the first Agent with the number of properties authored by the second one: 

<p style="background-color: Azure; padding: 5px;">
PREFIX a-cd: <https://w3id.org/arco/ontology/context-description/> <br>
PREFIX Agent: <https://w3id.org/arco/resource/Agent/> <br>
SELECT (COUNT(?object) AS ?n) <br>
WHERE { agent:f006a78cf246d5b7d73539da8eac78e3 a-cd:isAuthorOf ?object . <br>
 }  <br>
--> 82 results
 </p>
  
<p style="background-color: Azure; padding: 5px;">
PREFIX a-cd: <https://w3id.org/arco/ontology/context-description/> <br>
PREFIX Agent: <https://w3id.org/arco/resource/Agent/> <br>
SELECT (COUNT(?object) AS ?n) <br>
WHERE { agent:5fd98076b40717d5f8162f1580228220 a-cd:isAuthorOf ?object . <br>
 } <br>
--> 7 results
 </p>
  
The lower count (n. 7) of cultural properties authored by the second Agent, as compared to the general count (n. 82), confirms that this <a href= "https://w3id.org/arco/resource/Agent/f006a78cf246d5b7d73539da8eac78e3">IRI</a> focuses on a specific, more restricted subset of data related to Mantegna, likely within the regional context of Lombardy. 

Based on these considerations, we decide to focus for our project exclusively on the first agent, as it allows for a more general and richer exploration of the works of art. We therefore run the first SPARQL query of the project again, modifying it with the new information obtained:

<p style="background-color: Azure; padding: 5px;">
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> <br>
PREFIX arco: <https://w3id.org/arco/ontology/arco/> <br>
PREFIX a-cd: <https://w3id.org/arco/ontology/context-description/> <br>
PREFIX agent: <https://w3id.org/arco/resource/Agent/> <br>
SELECT DISTINCT * <br>
WHERE { <br>
?culturalProperty a arco:HistoricOrArtisticProperty ; <br>
rdfs:label ?title ; <br>
a-cd:hasAuthor agent:f006a78cf246d5b7d73539da8eac78e3 <br>
} <br>
ORDER BY ASC (?title) <br>
</p>
  
As expected, this time the query gives us a many more cultural properties, including Mantegna’ most famous artworks. Moreover, all the cultural properties retrieved belong to the class HistoricorArtisticProperty, and not the previously mentioned class PreparatoryWork:

![bild 3](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/b9a32e8a-3442-4487-b3aa-c6e6cf346b30)

This might imply that the very first, <a href= "https://w3id.org/arco/resource/Agent/12f2edbd230290b2abfb6c867ecef84b">preliminary Agent (prel)</a> we have retrieved is the one associated with the preparatory versions of the paintings, while this one is connected to their final, “official” versions. While the first agent is already linked to the second one through <i>owl:sameAs</i>, we could ensure that the second agent is also linked back to the first one, thus specifying that they refer to the same entity. This would make sure that the relationship is bidirectional: 

<https://w3id.org/arco/resource/Agent/12f2edbd230290b2abfb6c867ecef84b> <br>
owl:sameAs <br>
<https://w3id.org/arco/resource/Agent/f006a78cf246d5b7d73539da8eac78e3> <br>

Following these considerations, we believe it could also be useful to link the preparatory works to their final versions or vice versa. Our question is: are there any properties in ArCo that define this type of relationship? To answer it, we research in ArCo's Documentation to identify related properties. Such a property might be found in the Context Description module of the ArCo ontology. We find out that, as a matter of fact, this object property already exists:

<a href= "https://w3id.org/arco/ontology/context-description/hasRelatedWork">a-cd:hasRelatedWork</a> <br>

![bild 4](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/086aeb49-963b-467c-8dc5-3da916db53a3)

To find out if any of the completed artworks authored by Mantegna is linked to the preparatory works through this property, or vice versa, if the preparatory works are related to the completed versions, we use the UNION clause in our query:

<p style="background-color: Azure; padding: 5px;">
PREFIX arco:<https://w3id.org/arco/ontology/arco/> <br>
PREFIX a-cd:<https://w3id.org/arco/ontology/context-description/> <br>
PREFIX agent: <https://w3id.org/arco/resource/Agent/> <br>
SELECT ?preparatoryWork ?historicOrArtisticProperty <br>
WHERE { <br>
 {?preparatoryWork a-cd:hasAuthor agent:12f2edbd230290b2abfb6c867ecef84b ; <br>
a-cd:isWorkRelatedTo ?historicOrArtisticProperty . <br>
 ?historicOrArtisticProperty a-cd:hasAuthor agent:f006a78cf246d5b7d73539da8eac78e3 . } <br>
UNION <br>
{?historicOrArtisticProperty a-cd:hasRelatedWork ?preparatoryWork ; <br>
a-cd:hasAuthor agent:f006a78cf246d5b7d73539da8eac78e3 . <br>
?preparatoryWork a-cd:hasAuthor agent:12f2edbd230290b2abfb6c867ecef84b . } <br>
} <br>
</p>
  
Since we obtain no results, we use ASK to test if the property a-cd:hasRelatedWork is present at all within the ArCo ontology:

<p style="background-color: Azure; padding: 5px;">
PREFIX arco: <https://w3id.org/arco/ontology/arco/> <br>
PREFIX a-cd: <https://w3id.org/arco/ontology/context-description/> <br>
ASK <br>
{ <br>
  ?s a-cd:isRelatedWork ?o . <br>
} <br>
</p>
  
The query result is false, indicating that no triple using the a-cd:isWorkRelatedTo property exists within the ArCo KG. This suggests that introducing such triples in the context of Mantegna’s artwork might be relevant for representing these specific relationships between them. As an example, we propose two triples which connect the preparatory work (previously found among the list generated by our first query) whose subject is “Cristo Morto”, with the <a href= "https://w3id.org/arco/resource/HistoricOrArtisticProperty/0300180068">final painting</a>.

PROPOSITION OF NEW TRIPLES:

<b>1.Triple:</b><br>
https://w3id.org/arco/resource/HistoricOrArtisticProperty/0300180068 --> Subject <br>
a-cd:hasRelatedWork --> Predicate <br>
https://w3id.org/arco/resource/PreparatoryWork/0300182725-dipinto --> Object <br>

<b>2.Triple:</b> <br>
https://w3id.org/arco/resource/PreparatoryWork/0300182725-dipinto --> Subject <br>
a-cd:isRelatedWork --> Predicate <br>
https://w3id.org/arco/resource/HistoricOrArtisticProperty/0300180068 --> Object <br>

<div id="specific-section"><a name="custom-anchor"></a>
<h4 style="color:blue ;">3. Cristo Morto, Andrea Mantegna</h4></div>

Following this preliminary phase, we have decided to focus more specifically on two of his paintings that appeared in need of further enrichment. Consequently, the next two sections will be devoted to the methodology, results and analysis of “Cristo Morto” and “San Giorgio e il drago”.

<p style="background-color: Azure; padding: 5px;">
PREFIX arco: <https://w3id.org/arco/ontology/arco/> <br>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> <br>
SELECT DISTINCT ?property ?value <br>
WHERE { <br>
?cp a arco:HistoricOrArtisticProperty ; <br>
rdfs:label ?label; <br>
?property ?value . <br>
FILTER(REGEX(?label, "cristo morto nel sepolcro e tre dolenti. compianto sul cristo morto ", "i")) <br>
} <br>
</p>

![bild 1a](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/edc48011-8187-4626-be5b-6bde9c05ab47)

Parallelly, we decided to query the LLMS to help us gather relevant information about the piece of art, with the intention of comparing it with the results of our last query and identifying gaps or incomplete information. 

![bild2a](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/6c01961e-32da-4555-9d5f-45f2335e662c)

![bild3a](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/3b59f8f8-6e60-4d13-b90d-a70a76be1b17)

By examining all the existing properties and values and comparing it with the information that the LLMS gave us, one of the first things we noticed could be improved was the date of the painting. As illustrated by Gemini (and partially ChatGPT too), the date of the painting is still uncertain, with two possible dates being attributed to it. However, this aspect is not taken into account in ArCo. At this point, our question was: are there any properties or classes in ArCo that allow us to describe the presence of a second/alternative date attributed to a cultural property?
Our next step was then to check within the Context Description ontology of ArCo. Its analysis led us to discover that one of the sub-classes of the class Dating is precisely Alternative dating: 

![bild4a](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/dd02648c-e117-4594-94ac-7ee22827b0ed)

In other words, Alternative dating is a class that further allows to classify the type of Dating by specifying more in detail whether it is an obsolete dating, a different dating, etc. Since we observed that the class Dating is range of the property a-cd:hasDating, we could infer that Dating is used in triples where it is the object of the property mentioned. We could also infer that, since Alternative Dating is a sub-class of Dating, it inherits all its characteristics and properties, including a-cd:hasDating.  This is why we decided to build a SPARQL query to check whether or not there were cultural properties linked to Alternative Dating through the property a-cd:hasDating:  

<p style="background-color: Azure; padding: 5px;">
PREFIX arco: <https://w3id.org/arco/ontology/arco/> <br>
PREFIX a-cd: <https://w3id.org/arco/ontology/context-description/> <br>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> <br>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> <br>
SELECT * <br>
WHERE { <br>
  ?culturalProperty a-cd:hasDating ?dating . <br>
  ?dating rdf:type a-cd:AlternativeDating. <br>
 OPTIONAL { ?dating rdfs:label ?datingLabel . } <br>
} <br>
</p>
  
The query gave us no results, even if there were no syntax errors. For this reason, we decided to broaden the query and ask for a simple list all instances of Alternative Dating to see if any exists:

<p style="background-color: Azure; padding: 5px;">
PREFIX a-cd: <https://w3id.org/arco/ontology/context-description/> <br>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> <br>
SELECT ?dating <br>
WHERE { <br>
  ?dating rdf:type a-cd:AlternativeDating . <br>
} <br>
</p>
  
Since even this basic query returned no results, we became inclined to believe that the dataset may include no instances of this class in ArCo. However, we still decided to proceed, because the class exists in the ontology and because of the perception that such an implementation might enrich the knowledge graph. 
Following this reasoning, we created a new triple which links the Cristo Morto to the new Alternative Dating. The IRI and the literal we used to represent the new class was invented using as a model the first, “official” Dating of the artwork. 

 NEW TRIPLE 1
•	https://w3id.org/arco/resource/HistoricOrArtisticProperty/0300180068  Subject (Cristo Morto)
•	a-cd:hasDating  Predicate
•	https://w3id.org/arco/resource/AlternativeDating/0300180068  Object. 
The literal of the Alternative Dating is Cronologia 2 del bene 0300180068 (the code of the cultural property). 

After the creation of the new triple and the Alternative Dating page/IRI, we needed to specify the type of Alternative Dating we are introducing. For this purpose, we used LLMS to help us, with a combination of zero-shot and chain of thought prompting technique: 

Q: Andrea Mantegna's artwork "Cristo Morto" has two different possible datings: 1470-1474 ca. or 1483 ca. The alternative date is represented by the following IRI: https://w3id.org/arco/resource/AlternativeDating/0300180068.  The property describing the type of alternative dating is a-cd:hasAlternativeDatingType. The object of the property is a-cd:DifferentDatingType. The 3 possible types are: 1. a-cd:OtherMethodOfDating 2. a-cd:DifferentDating 3. a-cd:ObsoleteDating Which of these 3 object properties is the appropriate one for a triple?
A: Let’s think step by step.

CHAT GPT:

![bild5a](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/840c71f1-2f21-4b9c-8f42-355f04708414)

GEMINI:

![bild6a](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/b985eca4-3aed-4775-813c-a8a5a7c2ceeb)

Both ChatGPT and Gemini correctly identified the object of the new triple as “a-cd:differentDating. As a result, we decided to use it as the object of our new triple: 

NEW TRIPLE 2
•	https://w3id.org/arco/resource/AlternativeDating/0300180068  Subject
•	a-cd:hasAlternativeDatingType  Predicate
•	a-cd:differentDating  Object

The next passage was linking our Alternative Date to the Event of its creation, which would allow us to specify the precise date we wanted to include. We retrieved the property from ArCo’s documentation, among those properties of which Dating is the subject in triples: a-cd:hasDatingEvent. As far as the object is concerned, we continued to use, as a model for its creation, the Dating Event that was already present in relation to the Cristo Morto.

NEW TRIPLE 3:

•	https://w3id.org/arco/resource/AlternativeDating/0300180068  Subject
•	a-cd :hasDatingEvent  Predicate 
•	https://w3id.org/arco/resource/Event/0300180068-creation-2   Object 
The literal of our Dating Event is Realizzazione 2 del bene 0300180068 

At this point, in order to have an idea of which property and object were the most suitable to link our Event to its specific time (1483 ca.), we constructed a general SPARQL query to find the properties and objects related to the Dating Event that already existed in ArCo for the Cristo Morto. More specifically, the query would retrieve all triples where this entity was the subject, which is what we needed:

<p style="background-color: Azure; padding: 5px;">
PREFIX arco: <https://w3id.org/arco/ontology/arco/> <br>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> <br>
SELECT ?predicate ?object <br>
WHERE { <br>
<https://w3id.org/arco/resource/Event/0300180068-creation-1>  ?predicate  ?object . <br>
 } <br>
</p>
    
![bild](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/2230244b-710a-492e-ae1b-bec3770964a8)

From the list presented, we were then able to identify the predicate (a-cd:specificTime) and object ( ti:TimeInterval) we needed for our last triple, although we has to modify the time interval.

NEW TRIPLE 4:
•	https://w3id.org/arco/resource/Event/0300180068-creation-2    Subject
•	a-cd :specificTime  Predicate
•	https://w3id.org/arco/resource/TimeInterval/ca-1480-ca-1483  Object (Literal : ca 1480 - ca 1483). 
Since a time interval is apparently the only possibility, we included a slightly larger span of time, from 1480 to 1483. 

Finally, the last step was the creation of the new page of our Alternative Date, whose structure mirrors the style and content of the following example page:

![bild8](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/5fff03d8-1cb6-40f2-905a-e9bc67d99e88)

With all the information and triples gathered, this is the final page of the Alternative Dating of our cultural property: 
Cronologia 2 del bene 0300180068
https://w3id.org/arco/resource/Dating/0300180068-1ENTITÀ DI TIPO: Dating
rdfs:label
Cronologia 2 del bene 0300180068 / Dating 2 of cultural property 0300180068

l0:name
Cronologia 1 del bene 0300180068 / Dating 2 of cultural property 0300180068

rdf:type
a-cd:AlternativeDating

a-cd:hasAlternativeDatingType
a-cd:DifferentDating

a-cd:hasDatingEvent
<https://w3id.org/arco/resource/Event/0300180068-creation-2>
Realizzazione 2 del bene 0300180068


Next, we decided to look for cultural events related to this masterpiece using the following query:

<p style="background-color: Azure; padding: 5px;">
PREFIX cis: <http://dati.beniculturali.it/cis/> <br>
PREFIX a-cd: <https://w3id.org/arco/ontology/context-description/> <br>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> <br>
PREFIX arco: <https://w3id.org/arco/ontology/arco/> <br>
PREFIX agent: <https://w3id.org/arco/resource/Agent/> <br>
SELECT DISTINCT ?culturalEvent ?culturalProperty ?label <br>
WHERE{ <br>
?culturalEvent cis:involvesCulturalEntity ?culturalProperty . <br>
?culturalProperty a-cd:hasAuthor agent:f006a78cf246d5b7d73539da8eac78e3 ; <br>
a arco:HistoricOrArtisticProperty ; <br>
rdfs:label ?label . <br>
FILTER(REGEX(?label, "Cristo morto nel sepolcro e tre dolenti, compianto sul Cristo morto", "i")) <br>
} <br>
</p> 

The results of this query were just two, however we noticed that they were related to the same event: “Gonzaga. La Celeste Galleria”. We thus remarked that no information was provided about the exact location of the event. To retrieve this missing information, we used the zero-shot prompting technique on Chat GPT. The exact prompt was: “Where did the event "Gonzaga, La Celeste Galleria" take place?” and this was the answer:

![bild9](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/4b9adb47-8ba2-43be-9689-54bfa1371cb5)

Therefore, we decided to enrich the ArCo ontology by inserting more details about this event and by building a new triple which included its exact location. 
At this point, we needed to find the IRI of Palazzo Te; for this reason, we build the following SPARQL query: 

<p style="background-color: Azure; padding: 5px;">
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> <br>
PREFIX cis: http://dati.beniculturali.it/cis/ <br>
SELECT * <br>
WHERE { <br>
?Site rdfs:label ?label . <br>
 FILTER (REGEX(?label, "Palazzo Te", "i") ) <br>
} <br>
</p>

We found two different IRIs, one referring to the Museo Civico of Palazzo Te and the other simply referring to Palazzo Te: 

1. <a href= "https://w3id.org/arco/resource/Lombardia/CulturalInstituteOrSite/df850573204fac1a1938c8ecbd703b30"> IRI Museo Civico</a> <br>
2. <a href= "https://w3id.org/arco/resource/Lombardia/Site/88bbeb320f82f33c71368ac984b74f06"> IRI Palazzo Te</a>

Considering that we were dealing with an event, we opted for the IRI of Palazzo Te, estimating that it indicates the site in a more general sense and could hence produce a wider range of results. To find the right triple, we questioned Chat GPT again, and we also included another LLM, that is, Gemini. This time, we employed a few-shot prompting technique and we asked:

In RDF the sentence Cristo Morto by Mantegna is kept in Pinacoteca di Brera is expressed: 
Subject: Cristo Morto = https://w3id.org/arco/resource/HistoricOrArtisticProperty/0300180068  
Predicate: a-loc:hasCulturalInstituteOrSite 
Object: Pinacoteca di Brera = https://w3id.org/arco/resource/CulturalInstituteOrSite/4f94cfc32b33b17e12a1cbe848c08c75   
And the sentence: Camera degli stucchi, Divinità dell'Olimpo, Corteo militare is kept in Museo Civico Palazzo Te is expressed:
Subject:https://w3id.org/arco/resource/Lombardia/HistoricOrArtisticProperty/MN020-00071_R03
Predicate:a-loc:hasCulturalInstituteOrSite
Object: Museo Civico Palazzo Te: https://dati.beniculturali.it/lodview-arco/resource/Lombardia/CulturalInstituteOrSite/df850573204fac1a1938c8ecbd703b30
Now considering the previous sentences, can you write me a triple in RDF using the Arco ontology: the event Gonzaga La celeste Galleria was held in Palazzo Te?
 
The results were the following: 

GEMINI:
![bild10](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/7acfcf88-8d7e-4243-ab27-df89298bd6e8)

CHATGPT:
![bild11](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/c6ff9d63-3297-440a-a62a-32a874df4e08)

Gemini used the wrong IRI for Palazzo Te. However, we noticed that it understood that the predicate “was held “ is different from “is kept” and tried to guess an appropriate predicate for the sentence: the event Gonzaga La celeste Galleria was held in Palazzo Te by proposing “a-loc:heldAtLocation. On the contrary, ChatGPT is not able to understand that the predicate has to be different and creates a triple with the same predicate: a-loc:hasCulturalInstituteOrsite.
Now, we needed to verify if the predicate a-loc:heldatLocation was an appropriate property in the ArCo ontology. Exploring the Cultural Events and Exhibitions ontology of ArCo, we could not find the previous predicate. However, we discovered that among the properties related to the class “Cultural Event”, the property “cis:isHostedBySite” is included, and it refers to the site that hosts an event:

![bild12](https://github.com/KevinITS-site/KevinITS-site.github.io/assets/172382434/ccacb211-b52b-431e-9174-b29d57436754)

We then checked whether and how the predicate cis:is HostedBySite was employed in ArCo using the following query:

<p style="background-color: Azure; padding: 5px;">
PREFIX cis: <http://dati.beniculturali.it/cis/> <br>
SELECT DISTINCT * <br>
WHERE { <br>
  ?subject cis:isHostedBySite ?object . <br>
} <br>
</p>
  
Based on the many instances of this property we found in Arco which connect cultural events with the sites that host them, we believe it is also important to introduce a similar triple for our event:

CulturalEvent: Gonzaga. La Celeste Galleria.  https://w3id.org/arco/resource/CulturalEvent/a5cc0077c01891152d8d380f41ebed0e  Subject 
is hosted by site cis:isHostedBySite  Predicate 
Site:Palazzo Te https://w3id.org/arco/resource/Lombardia/Site/88bbeb320f82f33c71368ac984b74f06  Object

<div style="margin-top: 80px;"></div> 

<div id="specific-sections"><a name="c-anchor"></a>
<h4 style="color:blue; font-weight: bold;">4. San Giorgio e il drago, Andrea Mantegna</h4>

<div style= "text-align: center;">
<img src="https://github.com/capa46/project/assets/170109035/9e13c0ed-731d-459a-b603-5eba791f84be" width="200" height="400">
</div>





