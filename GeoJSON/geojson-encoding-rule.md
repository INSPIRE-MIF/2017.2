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
    * Technical Limitations
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
    * Alternative Coordinate Reference Systems
    * Identifiers
* [INSPIRE Theme Encoding Rules](#inspire-theme-encoding-rules)

## Preface

This document is the outcome of *[Action 2017.2](https://webgate.ec.europa.eu/fpfis/wikis/x/aAKOE) on alternative encodings for INSPIRE data*. 

The action aimed at defining alternative encoding rules (mainly for the purpose of viewing/analysis in mainstream GIS systems) for a number of selected application schemas and a template and procedure for proposing and endorsing additional encoding rules in the future.

Proposals for alternative encodings rules were collected through an open call on the MIG collaboration platform and prioritised by Member State representatives in a survey. The results of the survey clearly showed support for GeoJSON as a possible alternative encoding. In addition, also simplified GML, database formats (geopackage, PostGIS, ESRI Geodatabase) and linked data had significant support. Further proposals included also GeoSciML as an alternative encoding for GE and MR.

In the 48th MIG-T meeting, it was agreed to continue the 2017.2 work in a sub-group focussing on the following tasks:

- developing an encoding rule for GeoJSON (as a first example)
- developing generic rules / approaches for simplifying the INSPIRE data models (which will be useful for a number of alternative encodings)
- developing the overall procedure for proposing and endorsing additional encodings 

The work of the action encompassed the creation of generic encoding rules for GeoJSON as well as specific encoding rules for the INSPIRE themes Addresses (including `GeographicalName` properties) and Environmental Monitoring Facilities (including O&M properties). These encoding rules will be maintained as separate INSPIRE Good Practice documents, and in the future additional theme-specific encoding rules may be developed by thematic communities and proposed for endorsement by the MIG following the INSPIRE Good Practice procedure.

This work is also related to `2017.3`, where a major outcome is a detailed view on the capabilities of various GIS software of working with INSPIRE data (called [CanIUse](https://github.com/INSPIRE-MIF/caniuse/)), encoded in GML or GeoJSON.

## Introduction

This section describes what this document contains and what the high-level objective of this encoding is.

GeoJSON is an open standard format designed for representing simple geographical features, along with their non-spatial attributes. It is based on JSON, the JavaScript Object Notation. The body of the specification deals with describing GeoJSON Geometry Objects. These may be points (which can be used for features like addresses and locations), line strings (e.g. for streets, highways, boundaries), polygons (countries, provinces, tracts of land), and multi-part collections of these types.

GeoJSON features need not represent entities of the physical world only; mobile routing and navigation apps, for example, might describe their service coverage using GeoJSON.

The GeoJSON format has originally been defined by an Internet working group of developers who needed a solution to encode geometries for use in web applications. It has since been formalised by the IETF, a standards organisation which develops specifications concerning the Internet as [RFC 7946](https://tools.ietf.org/html/rfc7946).

Within INSPIRE, this encoding rule can be to encode data from several themes, with a focus on usability of the data in GIS desktop and web clients such as ArcMap, QGIS, OpenLayers, Leaflet, FME and hale studio. It can serve as an *alternative encoding* that can be used instead of the default encoding for simple data, where there is no information loss. In other cases, this GeoJSON encoding may serve as an *additional* encoding only.

## Scope

This sections describes the scope of the INSPIRE UML-to-GeoJSON encoding rule. GeoJSON is not equally well suited for all themes and use cases.

### Use Cases

This encoding rule specifically addresses data usability in web and desktop client software, such as ArcMap, QGIS, Leaflet and OpenLayers. It optimizes usage of INSPIRE data for mapping and geoprocessing in such applications.

The encoding rule is also developed with the best practices for [Spatial data on the Web](https://www.w3.org/TR/sdw-bp/) and the [WFS 3.0 standard](https://github.com/opengeospatial/WFS_FES) in mind, for which it should provide a complementary format. 

### Coverage of INSPIRE Themes

For each theme to be covered, a specific GeoJSON Encoding Rule is provided. These can reside in subfolders in the same repository as this general encoding rule (e.g. [`ads`](./ads/) and [`efs`](./efs/)), but can also be maintained in other places.

### Technical Issues

This encoding rule addresses specific technical issues that have been problematic when using the default encoding:

* Most GIS software cannot fully make use of non-smple attributes and nested structures for styling, processing and filtering;
* Multiple values per (complex) properties cannot be used fully in ArcGIS and other GIS tools;
* References to other features often cannot be resolved by GIS tools; Propertes of referenced features cannot be used in styling or for filtering ;
* Abstract geometry types for an object mean that a wide range of different geometries can be used for any single feature class;
* Mixed geometry types in a FeatureCollection are usually not supported.

### Technical Limitations

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
* [INSPIRE Drafting Team Data Specifications. D2.7: Guidelines for the encoding of spatial data, Version 3.3](http://inspire.ec.europa.eu/documents/guidelines-encoding-spatial-data)

## Terms and Definitions

Terms and Definitions can be found in the [Glossary](../glossary.md) document.

## Schema Conversion Rules

INSPIRE defines the conceptual model using UML.

The default encoding rule maps this UML model to XML Schema. For JSON, [JSON Schema](https://json-schema.org/) can be used to perform simple validation on JSON documents.  

NOTE At this point, [JSON Schema](https://json-schema.org/) is not used in any of the targeted GIS tools. We thus do not use it normatively. Theme-specific GeoJSON Encoding Rules may use JSON Schema to provide a formal definition of the encoded data structures, and to help develop executable test suites. 

In this encoding rule, we take a two-step approach, where we apply model transformations on the level of the conceptual model. This model can then be encoded in simple GeoJSON using the general schema and instance conversion rules laid out in the next sections.

### Types

#### Feature types 

All types that have the stereotype `<<featureType>>` are converted to GeoJSON objects. The typenames remain as they are. 

Where a class has one attribute with a geometry type, this attribute will be mapped to the `geometry` property in GeoJSON, while all other properties (attributes and association roles) will be mapped to properties inside the `properties` sub-object. Where a class has more than one Geometry property, a theme-specific profile has to define which geometry property is the "default" geometry that should be mapped to the `geometry` property in GeoJSON. Additional geometry properties can either be mapped to additional GeoJSON objects, or they can be retained in the set of `properties`.  

#### Data Types

All data types are mapped to JSON objects, where properties of the type are directly added to the root object. Their typenames remain as they are.

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

ISO 19107 defines a set of Geometry types, which need to be mapped to the types available in GeoJSON. 

NOTE Not all types can be mapped to GeoJSON; if a data set requires such a type, it cannot use this encoding rule as an alternative encoding rule.

| ISO 19107 type | GeoJSON datatype | Conversion Notes | 
| ------ | ----- | ----- |
| GM_Aggregate      | GeometryCollection | Limitations apply as to which types in the collection can be included. |
| GM_Curve          | LineString | In GML, Curves can also be nonlinear segments or arcs. GeoJSON only supports linear segments. |
| GM_MultiCurve     | MultiLineString | In GML, Curves can also be nonlinear segments or arcs. GeoJSON only supports linear segments. |
| GM_MultiPoint     | MultiPoint |  |
| GM_MultiPrimitive | not supported | `GM_MultiPrimitive` is an abstract type. |
| GM_MultiSurface   | MultiPolygon |  |
| GM_Object         | Any GeoJSON Geometry type | `GM_Object` is an abstract type, any GeoJSON geometry can be used. |
| GM_Point          | Point |  |
| GM_PolyhedralSurface | not supported | At this point, this specification does not support 3D meshes. |
| GM_Primitive      | Any GeoJSON Geometry type | `GM_Primitive` is an abstract type, any GeoJSON geometry can be used. |
| GM_Surface        | Polygon | A `GM_Surface` can have many SurfacePatches, it is thus mapped to MultiPolygon. |
| GM_Tin            | not supported | A TIN without triangulation could be converted to a MultiPoint object. |
| GM_Triangle       | Polygon |  |

#### ISO 19108 - Temporal types

For types from ISO 19108 used in INSPIRE schemas, suitable mappings need to be found on a case-by-case basis. The default should be to use the [Simple Period](/model-transformations/SimplePeriod.md) substitution rule.

#### ISO 19115 - Metadata types

For types from ISO 19115 used in INSPIRE schemas, suitable mappings need to be found on a case-by-case basis. For `CI_Citation`, the [Simple Citation](/model-transformations/SimpleCitation.md) substitution rule can be applied.

#### Abstract Types as property types

Where an abstract type with multiple concrete sub-types is used as a property type, a suitable choice of a concrete subtype should be made on a case-by-case basis. As an example, limiting the potential geometry types in this way can make processing easier.

#### Union Types

A `union` represents a choice between multiple properties with potentially different value types, such as in the AreaOfResponsibilityType, where there are options such as `areaOfResponsibilityByAdministrativeUnit` and `areaOfResponsibilityByNamedPlace`. The multiplicity of these options may also differ.

For Union Types used in INSPIRE models, suitable mappings need to be found on a case-by-case basis.

#### Enumerations and Code Lists

No mapping for code lists and enumerations is required. Their values shall be identified by (ideally resolvable) HTTP URIs.

NOTE The INSPIRE Registry can provide the JSON representation of the code list and its entries.

### Properties

Property names remain as they are.

If a property has a cardinality > 1, a suitable mapping needs to be found on a case-by-case basis. There is a [model transformation rule](/model-transformations/ExtractPrimitiveArray.md) that extracts a single value from a complex property and builds a JSON array which should be used if the number of occurences of such a property can be very high. 

Properties that represent values form code lists are encoded using the `SimpleCodelistReference` [rule described here](/model-transformations/SimpleCodelistReference.md).

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

### Character Encoding

The character encoding of all data encoding in GeoJSON shall be UTF-8.

### Coordinate Reference Systems 

As per the requirements of the GeoJSON - IETF RFC 7946 specification, the default CRS for any data set delivered using this encoding rule is a geographic coordinate reference system, using the World Geodetic System 1984 (WGS 84) datum, with longitude and latitude units of decimal degrees, unless there is prior arrangement. This is equivalent to the coordinate reference system identified by the Open Geospatial Consortium (OGC) URN `urn:ogc:def:crs:OGC::CRS84`.

NOTE As INSPIRE mandates the use of the European Terrestrial Reference System 1989  (ETRS89, see [Requirement 1](https://inspire.ec.europa.eu/reports/ImplementingRules/DataSpecifications/INSPIRE_Specification_CRS_v2.0.pdf)) for the areas within the geographical scope of ETRS89 and both CRS84 and ETRS89 use the GRS 80 ellipsoid (although with minor enhancements), we shall assume CRS84 to be equivalent to ETRS89. If, for any dataset, this assumption would be problematic, then GeoJSON cannot serve as an alternative encoding rule for that dataset.

### Alternative Coordinate Reference System support

While the required Coordinate Reference System for any data encoded in GeoJSON is CRS84, a client may request delivery of a data set using a different projected reference system, as per the mechanism described in Requirement 8 in the [WFS 3.0 draft specification](https://github.com/opengeospatial/WFS_FES). 

An INSPIRE Download service delivering data encoded in GeoJSON shall be able to deliver projected geometries if a client requests these explicitly, at least for the spatial reference systems documented in section 6.3. of the data specifications that fall within the scope of this encodign specification. When delivering data that is not in [CRS 84](http://www.opengis.net/def/crs/OGC/1.3/CRS84), the GeoJSON data should include the `crs` member as defined in the deprecated (Draft 6 of the GeoJSON specification)[http://wiki.geojson.org/GeoJSON_draft_version_6].

### nilReason information

In the GeoJSON encoding rule, `nilReason` information shall not be maintained per feature, but rather in the dataset metadata. Properties that have `nil` values shall thus be ignored in the encoding process.

NOTE If, for any dataset, there is specific `nilReason` information per feature, then GeoJSON cannot serve as an alternative encoding rule for that dataset

### Identifiers

A spatial object encoded using the default encoding rule may have several properties that identify it:

* `gml:id`: This property with the `ID` property type is not present in the conceptual model, but mandatory for any spatial object encoded in GML. It represents a technical identifier that is unique within a document and can serve as the target of an anchor/reference.
* `gml:identifier`: This property with the `gml:CodeWithAuthorityType` property type is not present in the conceptual model, but inherited from the `AbstractGML` type. It represents an identifier that is unique within the codeSpace given and serves as the external identifier of the object.
* `inspireId:` This property with the type `IdentifierPropertyType` defines a unique, persistent domain identifier for the spatial object within the INSPIRE infrastructure.

These properties are mapped to the encoded GeoJSON object as follows:

| Default Encoding property | Property Type | GeoJSON Property | Property Type | Conversion Notes | 
| ------ | ----- | ----- | ----- | ----- |
| `gml:id` | ID | `id` | string |  |
| `gml:identifier` | CodeWithAuthorityType | `properties.identifier` | string | Can be omitted if empty in the source object. |
| `base:inspireId` | IdentifierPropertyType | `properties.inspireId.localid` | string |  |
|  |  | `properties.inspireId.namespace` | string |  |
|  |  | `properties.inspireId.versionId` | string | Can be omitted if empty in the source object. |

## INSPIRE Theme Encoding Rules

This document does not contain specific rules for each INSPIRE theme. These are maintained in separate documents to facilitate loosely coupled development cycles and groups.

Each of the theme-specific encoding rules defines at least one conformance class. Any conformance class in a theme encoding rule may define a number of model transformation rules that need to be applied before the encoding process. These transformations are documented in the [Model Transformation Rules](../model-transformations/TransformationRules.md) paper. They serve the purpose of adapting the conceptual model (UML) to better match the logical model of the target platform.
