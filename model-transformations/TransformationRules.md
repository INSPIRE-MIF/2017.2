# Model Transformations

## Introduction

The intent of this document is to describe multiple model transformation rules. These model transformations reduce complexity in encoded INSPIRE data, e.g. by reducing levels of aggregation, indirect referencing, using simple geometries and flattening structures such as arrays. As with Alternative Encodings, they have different objectives and scopes. A rule may be used with any number of encodings, including the default encoding, if applicable.

An Alternative Encoding may refer to any number of such model transformation rules in its conformance classes. For this purpose, each model transformation rule receives a unique identifier. For an Alternative Encoding to be the sole encoding, there may not be any information loss for the particular data set in question. Where there is information loss, such encoding may only be used as an Additional Encoding.

## Requirements for Model Transformations

Each Model Transformation is described by these properties:

- Name
- Unique Identifier
- Category
- Description
- Original vs. Transformed UML Model, where applicable
- Original instance in default encoding
- Transformed instance in default encoding, where applicable
- Model Transformation Rule
- Instance Transformation Rule
- Solved Usability issues
- Known Usability issues
- INSPIRE compliance conditions and reversibility
- Examples of use (Links to examples in the 2017.2 repository)
- Additional notes

## Catalogue of Model Transformations

This catalogue contains general model Simplification Rules we have identified so far. 

The catalogue also contains several Substitution Rules, where existing types such as `GeographicName` are replaced with less complex types. These types are added to the theme namespaces under draft schemas  (`https://inspire.ec.europa.eu/draft-schemas/`).

## SIMPLIFICATION RULES

### MT001: Flatten Nested Structures

[General Flattening of nested structures](./GeneralFlattening.md)

### MT002: Extract Primitive Arrays

[Extract Primitive Array](./ExtractPrimitiveArray.md)

### MT003: Flatten Associated Components Using Typenames

[Association/Aggregation to Composition with Hard Typing](./AssociatedComponentsHardType.md)

### MT004: Flatten Associated Components Using Codelist Values

[Association/Aggregation to Composition with Soft Typing](./AssociatedComponentsSoftType.md)

### MT006: Refer to Property Values by Reference

[Property Composition to Association](./PropertyCompositionToAssocation.md)

### MT00X (PROPOSED) Retain Nested Child Structures 

TBD RetainAdditionalNestedChildElements

### MT00X (PROPOSED) MTXXX: Fan-Out Feature Types to Multiple Feature 

TBD FanOutFeatureClasses

### MT00X (PROPOSED) Fan-Out Features by Geometry Type

TBD FanOutFeaturesByGeometryType

## SUBSTITUTION RULES

### MT005: Simple Geographic Name

[Simple Geographic Name](./SimpleGeographicName.md)

### MT007: Simple Citation

[Simple Citation](./SimpleCitation.md)

### MT008: Simple Codelist Reference

[Simple Codelist Reference](./SimpleCodelistReference.md)

### MT009: Simple Period

[Simple Period](./SimplePeriod.md)

### MT00X: European Legislation Identifier

[European Legislation Identifier](./EuropeanLegislationIdentifier.md)

## MT00X (PROPOSED) Abbreviate Prefix of Compound Property Names

TBD AbbreviateCompoundPropertyNames
