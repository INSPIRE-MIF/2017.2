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

#### Rule T1-R1: Flattening of complex structures

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
        <td>The complex structure of model elements can be reduced by applying a flattening method. The principle of the flattening is to derive a flat model structure by moving the nested child elements to its parent. The elements can be renamed to represent the former element path in the name of the resulting element and to avoid naming conflicts. The cardinality of the derived elements should be calculated from the cardinalities of the former element path. 
        If the upper bound of the resulting element multiplicity is not unbounded, but greater than 1, it is possible to create a single element for each occurrence to avoid elements with multiple value occurrence. In this case, the derived element name could be suffixed by an index value. when applied recursively, this method flattens the structure of multiple levels.
        </td>
    </tr>
    <tr>
        <td>UML Model</td>
        <td></td>
    </tr>
    <tr>
        <td>Example instance in default encoding:</td>
        <td></td>
    </tr>
    <tr>
        <td>Example instance in simplified encoding:</td>
        <td></td>
    </tr>
    <tr>
        <td>Model transformation rule: </td>
        <td></td>
    </tr>
    <tr>
        <td>Instance transformation rule:</td>
        <td></td>
    </tr>
    <tr>
        <td>Solves usability issues:</td>
        <td></td>
    </tr>
    <tr>
        <td>Known usability issues:</td>
        <td></td>
    </tr>
    <tr>
        <td>Reversibility:</td>
        <td>Full</td>
    </tr>
</table>

Notes:

### Transformation 2: 2016.1 Fitness for purpose Annex III - Danish comments

Also in 2017, the Danish Agency for Data Supply and Efficiency (SDFE) conducted a study on how to simplify models to SImple Feature-0 level as far as possible. In part, this document also references the GDI-DE Study and suggests some refinements and alternate approaches to be taken.

## Evaluation of transformation methods for different use cases

## Selected Best Practices