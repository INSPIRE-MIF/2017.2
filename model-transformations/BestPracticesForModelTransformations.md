# Best practices for Model Transformations

## Introduction

The intent of this best practice paper is to describe multiple model transformation methods. These methods reduce complexity in encoded INSPIRE data, e.g. by reducing levels of aggregation, indirect referencing, using simple geometries and flattening structures such as arrays. As with alternate encodings, they have different objectives and scopes.

An Alternate encoding may refer to any number of such model transformation rules in its conformance classes. For this purpose, each model transformation rules receives a unique identifier.

## Requirements for Model Transformations

Model Transformations can be described either on the conceptual model level (UML to UML) or at the logical level (e.g. XML Schema to XML Schema). They can include a model language translation, such as going from XML Schema to JSON Schema.

## Catalogue of simplifying Model Transformations

This section contains a selection of examples for model transformations we have identified so far. Typically, a set of rules was identified from a single source or project.

### Project 1: GDI-DE Study on 2016.1 Fitness for purpose Annex III

In 2017, The GDI-DE investigated which changes could be made to the existing default encoding that would have significant impact on data usability. As a result of this study, a set of 13 recommendations were formulated. Not all of these address model transformations, and some are more specific than others.

The complete study is available [here](https://www.geoportal.de/SharedDocs/Downloads/DE/GDI-DE/Dokumente/FitnessForPurpose_RecommendationsForChanges.pdf?__blob=publicationFile).

#### Rule P1-REC001: Flattening of complex structures

<table>
<tr>
<td>Name of the Rule</td>
<td>Flattening of complex structures</td>
</tr>
<tr>
<td>Category</td>
<td>General model simplification rules</td>
</tr>
<tr>
<td>Description</td>
<td><p>The complex structure of model elements can be reduced by applying a flattening method. The principle of the flattening is to derive a flat model structure by moving the nested child elements to its parent. The elements can be renamed to represent the former element path in the name of the resulting element and to avoid naming conflicts. The cardinality of the derived elements should be calculated from the cardinalities of the former element path.</p> 
<p>If the upper bound of the resulting element multiplicity is not unbounded, but greater than 1, it is possible to create a single element for each occurrence to avoid elements with multiple value occurrence. In this case, the derived element name could be suffixed by an index value. When applied recursively, this method flattens the structure of multiple levels.</p>
</td>
</tr>
<tr>
<td>UML Model</td>
<td>TODO</td>
</tr>
<tr>
<td>Example instance in default encoding:</td>
<td>

```xml
    <gn:NamedPlace gml:id="NamedPlace_Example">
        <gn:beginLifespanVersion xsi:nil="true"/>
        <gn:geometry>
            <gml:Point gml:id="_d7180a8f-a590-44da-8b45-41d96d5cba5e" srsName="http://www.opengis.net/def/crs/EPSG/0/25832" srsDimension="2">
            <gml:pos>471979.2568 5564594.2444</gml:pos>
            </gml:Point>
        </gn:geometry>
        <gn:inspireId>
            <base:Identifier>
                <base:localId>NamedPlace_Example</base:localId>
                <base:namespace>https://www.examples.eu/</base:namespace>
            </base:Identifier>
        </gn:inspireId>
        <gn:localType xsi:nil="true"/>
        <gn:name>
            <gn:GeographicalName>
                <gn:language>deu</gn:language>
                <gn:nativeness xsi:nil="true"/>
                <gn:nameStatus xsi:nil="true"/>
                <gn:sourceOfName xsi:nil="true"/>
                <gn:pronunciation xsi:nil="true"/>
                <gn:spelling>
                    <gn:SpellingOfName>
                    <gn:text>München</gn:text>
                    <gn:script xsi:nil="true"/>
                    </gn:SpellingOfName>
                </gn:spelling>
            </gn:GeographicalName>
        </gn:name>
        <gn:name>
            <gn:GeographicalName>
                <gn:language>eng</gn:language>
                <gn:nativeness xsi:nil="true"/>
                <gn:nameStatus xsi:nil="true"/>
                <gn:sourceOfName xsi:nil="true"/>
                <gn:pronunciation xsi:nil="true"/>
                <gn:spelling>
                    <gn:SpellingOfName>
                    <gn:text>Munich</gn:text>
                    <gn:script xsi:nil="true"/>
                    </gn:SpellingOfName>
                </gn:spelling>
            </gn:GeographicalName>
        </gn:name>
        <gn:type xsi:nil="true"/>
    </gn:NamedPlace>
```
   
</td>
</tr>
<tr>
<td>Example instance in simplified encoding:</td>
<td>

```json
    {
        "inspireId.localId": "NamedPlace_Example",
        "inspireId.namespace": "https://www.examples.eu/",
        "name_1.language": "deu",
        "name_1.spelling.text": "München",
        "name_2.language": "eng",
        "name_2.spelling.text": "Munich"
    }
``` 

</td>
</tr>
<tr>
<td>Model transformation rule: </td>
<td></td>
</tr>
<tr>
<td>Instance transformation rule:</td>
<td>For each value, a property is created, so instance values can simply be copied.</td>
</tr>
<tr>
<td>Solves usability issues:</td>
<td>The flattened data can be filtered and symbolized easily in desktop GIS and web GIS software. The flattened data can be processed much easier by many tools, e.g. it can be converted to excel easily</td>
</tr>
<tr>
<td>Known usability issues:</td>
<td>Flattening of large arrays will lead to a very large number of properties on the first level. Some software and formats can only work with a limited number of properties on a layer (ArcMap has 65.534, shapefile is limited to 250), so this can limit usability in extreme cases. Some software also has limits on the length of property names (File Geodatabase = 64 characters, Shapefile = 11 characters).</td>
</tr>
<tr>
<td>Reversibility:</td>
<td>Full (if property names don't have to be shortened)</td>
</tr>
</table>

Notes: No notes.

### Transformation 2: 2016.1 Fitness for purpose Annex III - Danish comments

Also in 2017, the Danish Agency for Data Supply and Efficiency (SDFE) conducted a study on how to simplify models to SImple Feature-0 level as far as possible. In part, this document also references the GDI-DE Study and suggests some refinements and alternate approaches to be taken.

## Evaluation of transformation methods for different use cases

## Selected Best Practices
