# INSPIRE UML-to-GeoJSON encoding rule

`Version: 0.1`
`Date: 2019-03-29`

## Table of Contents

* [Preface](#preface)
* [Introduction](#introduction)
* [Scope](#scope)
    * Use Cases
	* Themes
    * Technical Issues
	* Cross-cutting INSPIRE requirements
* [Normative References](#normative-references)
* [Terms and Definitions](#terms-and-definitions)
* [Schema Conversion Rules](#schema-conversion-rules)
    * Types
    * Properties
    * Associations
* [Instance Encoding Rules](#instance-encoding-rules)
    * Requirements and Recommendations
    * Mapping from Conceptual Model to GeoJSON Logical Model
    * Alternate Coordinate Reference Systems
    * TODO Identifiers
* [INSPIRE Theme Encoding Rules](#inspire-theme-encoding-rules)

## Preface

This document is the outcome of *[Action 2017.2](https://webgate.ec.europa.eu/fpfis/wikis/display/InspireMIG/Action+2017.2+on+alternative+encodings+for+INSPIRE+data) on alternative encodings for INSPIRE data*. In that action, we defined alternative encoding rules for the purpose of viewing and analysing INSPIRE data in mainstream GIS systems. In addition to the development of this GeoJSON encoding rule, theme-specific rules have been developed. The lessons learnt during the creation of these specifications are documented in a template and procedure for proposing and endorsing additional encoding rules.

Specifically, the following tasks were part of this action:

> * Develop concrete proposals for alternative encodings
>     * In collaboration with thematic communities (through the Thematic Clusters platform and MIWP-14 sub-group), collect proposals for alternative encodings. These can be based on existing examples and/or on specific use cases and requirements. The proposals can be cross-cutting (i.e. cover all INSPIRE themes) or specific for one or several related themes.
>     * In agreement with the MIG-T, prioritise the collected examples and select a small number of proposals, for which alternative encodings will be developed by the action.
>     * For the selected examples, develop encoding rules that explain how (and/or under which conditions) the proposed encoding meets the requirements of the IRs. The action should also consider the potential loss of information for certain encodings and discuss whether such "lossy" encodings are meeting the IR requirements.
> * Define a template and procedure for proposing and endorsing additional encoding rules
>     * Based on the work on (1a), elaborate a template for proposals for additional encoding rules. The template should cover the actual encoding rule (including possible approaches for explicitly documenting mappings in UML), but also target use cases, expected benefits, known limitations and tools for conformity testing & validation.
>     * Develop a procedure for how additional encoding rules can be proposed using the template and checked/endorsed by the MIG, and how these are referred to from the existing data specification TGs.
>     * Develop a proposal for the update or maintenance of endorsed encoding rules.
>     * Create a repository of addition encoding rules that have been endorsed by the MIG.
>     * Develop a proposal for documenting the used encoding rules in data set/service metadata.

The work on this draft encoding rule encompassed the creation of specific encoding rules for the INSPIRE themes Addresses (including `GeographicalName` properties) and Environmental Monitoring Facilities (including O&M properties). These may be maintained separately in the future, and additional, theme-specific encoding rules may be developed by the MIG or the INSPIRE community.

## Introduction

This section describes what this document contains and what the high-level objective of this encoding is.

GeoJSON is an open standard format designed for representing simple geographical features, along with their non-spatial attributes. It is based on JSON, the JavaScript Object Notation. The body of the specification deals with describing GeoJSON Geometry Objects. These may be points (which can be used for features like addresses and locations), line strings (e.g. for streets, highways, boundaries), polygons (countries, provinces, tracts of land), and multi-part collections of these types.

GeoJSON features need not represent entities of the physical world only; mobile routing and navigation apps, for example, might describe their service coverage using GeoJSON.

The GeoJSON format has originally been defined by an Internet working group of developers who needed a solution to encode geometries for use in web applications. It has since been formalised as an [IETF internet standard](https://tools.ietf.org/html/rfc7946), a standards organisation, which develops specifications concerning the Internet.

Within INSPIRE, this encoding rule can be to encode data from several themes, with a focus on usability of the data in GIS desktop and web clients such as ArcMap, QGIS, OpenLayers, Leaflet, FME and hale studio. It can serve as an *alternative encoding* that can be used instead of the default encoding for simple data, where there is no information loss. In other cases, this GeoJSON encoding may serve as an *additional* encoding only.

## Scope

This sections describes the scope of the INSPIRE UML-to-GeoJSON encoding rule. GeoJSON is not equally well suited for all themes and use cases.

### Use Cases

This encoding rule specifically addresses data usability in web and desktop client software, such as ArcMap, QGIS, Leaflet and OpenLayers. It optimizes usage of INSPIRE data for mapping and geoprocessing in such applications.

The encoding rule is also developed with the best practices for [Spatial data on the Web](https://www.w3.org/TR/sdw-bp/) and the [WFS 3.0 standard](https://github.com/opengeospatial/WFS_FES) in mind, for which it should provide a complementary format. 

### Coverage of INSPIRE Themes

This encoding rule covers the following themes:

* Annex I: [Addresses](./ads/simple-addresses.md)
* Annex III: [Environmental Monitoring Facilities](./ems/simple-environmental-monitoring-facilities.md)

### Technical Issues

This encoding rule addresses specific technical issues that have been problematic when using the default encoding:

* Most GIS software cannot fully make use of non-smple attributes and nested structures for styling, processing and filtering;
* Multiple values per (complex) properties cannot be used fully in ArcGIS and other GIS tools;
* References to other features often cannot be resolved by GIS tools; Propertes of referenced features cannot be used in styling or for filtering ;
* Abstract geometry types for an object mean that a wide range of different geometries can be used;
* Mixed geometry types in a FeatureCollection are usually not supported;

In some cases such as the handling of high-cardinality properties, this encoding rule makes a trade-off, so not all issues are resolved. Implementers can apply additional model and instance transformation rules to make adjustments for specific data sets and environments.

The GeoJSON format cannot deal with 3D geometries and coverage/raster data, therefore this encoding rule cannot be used for those types of data.

### INSPIRE Requirements for Encoding Rules

The Implementing Rules on interoperability of spatial data sets and services (Commission Regulation (EU) No 1089/2010) lays down the following requirements for encoding rules:

> **Article 7 -- Encoding**
>
> 1. Every encoding rule used to encode spatial data shall conform to EN ISO 19118. In particular, it shall specify schema
> conversion rules for all spatial object types and all attributes and association roles and the output data structure used. 
> 2. Every encoding rule used to encode spatial data shall be made available.

D2.7 specifies more detailed requirements and recommendations for encoding rules. The following list lists the requirements from that document and shows which ones are also met in this encoding rule:

> * Requirement 12: ... documents shall be required to be encoded using UTF-8 as character encoding.

D2.7 also contains a relevant recommendation:

> * Recommendation 3: Encoding rules should be based on international, preferably open, standards.

## Normative References

This section contains references to standards documents and related resources.

* [GeoJSON - IETF RFC 7946](https://tools.ietf.org/html/rfc7946)
* [D2.7 INSPIRE DRAFTING TEAM “DATA SPECIFICATIONS.” D2.7: Guidelines for the encoding of spatial data, Version 3.3](http://inspire.ec.europa.eu/documents/guidelines-encoding-spatial-data)

## Terms and Definitions

Terms and Definitions can be found in the [Glossary](../glossary.md) document.

## Schema Conversion Rules

INSPIRE defines the conceptual model using UML.

The default encoding rule maps this UML model to XML Schema. For JSON, [JSON Schema](https://json-schema.org/) can be used to perform simple validation on JSON documents.  

NOTE At this point, [JSON Schema](https://json-schema.org/) is not used in any of the targeted GIS tools. We thus do not yet use it normatively, but to provide a formal definition of the encoded data structures, and to help develop executable test suites in future versions. 

In this encoding rule, we take a two-step approach, where we apply model transformations on the level of the conceptual model. This model can then be encoded in simple GeoJSON using the general schema and instance conversion rules laid out in the next sections.

### Types

#### General types 

Typenames remain as they are. All types that have the stereotype `<<featureType>>` are converted to GeoJSON objects. All other types are mapped to regular JSON objects, where properties of the type are directly added to the root object instead of being added to the `properties` subobject.

TODO split up into FT and DT sections with headings

#### ISO 19103 - Basic types

All property types are transformed to the simple types that JSON knows about: Number, String, Boolean and Object. The exact mapping from the UML model to the JSON datatypes is outlined in the following table:

| UML Model property type | JSON datatype | Conversion Notes | 
| ------ | ----- | ----- |
| CharacterString | string |  |
| LocalisedCharacterString | string | `LanguageCode` is added as a separate property. |
| Boolean | boolean |  |
| Integer | integer |  |
| Real | number |  |
| Decimal | number |  |
| DateTime | string | The string must follow the ISO 8601 format, including timezone information (e.g. `2008-10-31T15:07:38-05:00`). |
| Date | string | The string most follow the format `yyyy-mm-dd`. |
| Length | double | `uom` is added as a separate property. |
| Measure | double | `uom` is added as a separate property. |
| URI | string |  |
| URL | string |  |

Any other UML Model property type are to be mapped to `string`, with specific rules being defined on a case-by-case basis in each theme profile.

#### ISO 19107 - Geometry types

ISO 19107 defines a set of Geometry types, which need to be mapped to the types available in GeoJSON. Note that not all types can be mapped to GeoJSON; if an data set requires such a type, it cannot use this encoding rule as an alternative encoding rule.

| XML Schema datatype | GeoJSON datatype | Conversion Notes | 
| ------ | ----- | ----- |
| GM_Aggregate      | GeometryCollection | Limitations apply as to which types in the collection can be included. |
| GM_Curve          | LineString | In GML, Curves can also be nonlinear segments or arcs. GeoJSON only supports linear segments. |
| GM_MultiCurve     | MultiLineString | In GML, Curves can also be nonlinear segments or arcs. GeoJSON only supports linear segments. |
| GM_MultiPoint     | MultiPoint |  |
| GM_MultiPrimitive | not supported | `GM_MultiPrimitive` is an abstract type. |
| GM_MultiSurface   | Polygon |  |
| GM_Object         | not supported | `GM_Object` is an abstract type. |
| GM_Point          | Point |  |
| GM_PolyhedralSurface | not supported | At this point, this specification does not support 3D meshes. |
| GM_Primitive      | not supported | `GM_Primitive` is an abstract type. |
| GM_Ring           | Polygon | A `GM_Ring` is not intended to be used as a standalone geometry object. It is typically used to define an interior or exterior boundary in a Surface and is thus mapped to Polygon. |
| GM_Surface        | Polygon | A `GM_Surface` can have many SurfacePatches, it is thus mapped to MultiPolygon. |
| GM_Tin            | not supported | TODO A TIN without triangulation could be converted to a MultiPoint object. |
| GM_Triangle       | Polygon |  |

Where a class has one attribute with a geometry type, this attribute will be mapped to the `geometry` property in GeoJSON, while all other properties (attributes and association roles) will be mapped to properties inside the `properties`. A theme-specific profile has to define which geometry property is the "default" geometry that should be mapped to the `geometry` property in GeoJSON.

#### ISO 19108 - Temporal types

For types from ISO 19108 used in INSPIRE schemas, suitable mappings need to be found on a case-by-case basis. The default should be to use the [Simple Period](../model-transformation/SimplePeriod.md) substitution rule.

#### ISO 19115 - Metadata types

For types from ISO 19108 used in INSPIRE schemas, suitable mappings need to be found on a case-by-case basis. For `CI_Citation`, the [Simple Citation](../model-transformation/SimpleCitation.md) substitution rule can be applied.

#### TODO Abstract Types as property types



#### Inheritance

FIXME As `abstract` types cannot be encoded directly, the inheritance hierarchy is collapsed to the concrete types. Abstract types are then removed from the model.

#### Union Types

TODO Fix definition based on Input from Peter, correct example (from Heidi), add definition to glossary as well.

A `union` represents a choice between multiple properties with different value types, such as a `Reference` and a `Building`. They can have a multiplicity other than exactly 1.

For Union Types used in INSPIRE schemas, suitable mappings need to be found on a case-by-case basis.

#### Enumerations and Code Lists

TODO change to reflect SimpleCodelistRef implementation model
Enumerations and classes with the sterotype `<<Codelist>>` remain unchanged.

NOTE The INSPIRE Registry can provide the JSON representation of the code list.

### Properties

Property names remain as they are.

NOTE Namespace prefixes, as used in the default encoding, are not used in the GeoJSON encoding rule.

#### Properties with a `uom` attribute

The unit of measurement attribute (`uom`) on any property `x` has to be retained. It is transformed to a new property of the type with the name `x.uom`.

#### Arrays

Property types for properties with a cardinality greater than `1` and a simple property type (e.g. String, Integer, Float, ...) may use arrays of these simple types. More information is available in the [Extract Primitive Array](../model-transformation/ExtractPrimitiveArray.md) transformation rule.

#### Voidable

The stereotype `<<voidable>>` is not converted. If a property has no value, it may be dropped.

### Association Roles

Association roles are retained as they are, if they are not transformed using a profile-specific rule, such as [Inline associated or aggregated components using type names](../model-transformation/AssociatedComponentsHardType).

## Instance Encoding Rules

This section describes how the encoding is derived from the converted conceptual model, and describes which common rules have to be applied for this encoding rule.

### Common Rules

* `GEOJSON-REQ-01`: The character encoding of all data encoding in GeoJSON shall be UTF-8.
* `GEOJSON-REQ-02`: As per the requirements of the GeoJSON - IETF RFC 7946 specification, the default CRS for any data set delivered using this encoding rule is a geographic coordinate reference system, using the World Geodetic System 1984 (WGS 84) datum, with longitude and latitude units of decimal degrees, unless there is prior arrangement. This is equivalent to the coordinate reference system identified by the Open Geospatial Consortium (OGC) URN `urn:ogc:def:crs:OGC::CRS84`.

NOTE As INSPIRE mandates the use of the European Terrestrial Reference System 1989  (ETRS89, see [Requirement 1](https://inspire.ec.europa.eu/reports/ImplementingRules/DataSpecifications/INSPIRE_Specification_CRS_v2.0.pdf)) for the areas within the geographical scope of ETRS89 and both CRS84 and ETRS89 use the GRS 80 ellipsoid (although with minor enhancements), we shall assume CRS84 to be equivalent to ETRS89. If, for any dataset, this assumption would be problematic, then GeoJSON cannot serve as an alternative encoding rule for that dataset.

* `GEOJSON-REQ-03`: In the GeoJSON encoding rule, `nilReason` information shall not be maintained per feature, but rather in the dataset metadata. Properties that have `nil` values shall thus be ignored in the encoding process.

NOTE If, for any dataset, there is specific `nilReason` information per feature, then GeoJSON cannot serve as an alternative encoding rule for that dataset

### Alternate Coordinate Reference System support

While the required Coordinate Reference System for any data encoded in GeoJSON is CRS84, a client may request delivery of a data set using a different projected reference system, as per the mechanism described in Requirement 8 in the [WFS 3.0 draft specification](https://github.com/opengeospatial/WFS_FES). 

* `GEOJSON-REC-01`: An INSPIRE Download service delivering data encoded in GeoJSON shall be able to deliver projected geometries if a client requests these explicitly, at least for the spatial reference systems documented in section 6.3. of the data specifications that fall within the scope of this encodign specification. When delivering data that is not in [CRS 84](http://www.opengis.net/def/crs/OGC/1.3/CRS84), the GeoJSON data should include the `crs` member as defined in the deprecated (Draft 6 of the GeoJSON specification)[http://wiki.geojson.org/GeoJSON_draft_version_6].

## INSPIRE Theme Encoding Rules

This document does not contain specific rules for each INSPIRE theme. These are maintained in separate documents to facilitate loosely coupled development cycles and groups.

Each of the theme-specific encoding rules defines at least one conformance class. Any conformance class in a theme encoding rule may define a number of model transformation rules that need to be applied before the encoding process. These transformations are documented in the [Model Transformation Rules](../model-transformations/TransformationRules.md) paper. They serve the purpose of adapting the conceptual model (UML) to better match the logical model of the target platform.