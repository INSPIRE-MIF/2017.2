# Alternate Encoding for INSPIRE Data: GeoJSON

## Table of Contents

* Introduction
* Scope
    * Use Cases
	* Themes
	* Cross-cutting INSPIRE requirements
* Conformance
* Normative References
* Terms and Definitions
* General Encoding rules
    * Requirements and Recommendations
* Conformance Classes
    * Core GeoJSON support
    * Alternate CRS support
    * Array property support
* Mapping to the Default INSPIRE encoding
    * This encoding to INSPIRE GML
	* INSPIRE GML to this encoding
* Annex I (Normative/Informative): Abstract / Executable Test Suite
* Annex II (Informative): Compatibility Tables 
* Annex III (Informative): Examples

## Introduction

*Describe what this document contains and what the high-level objective of this encoding is. Clarify the objectives, and ideally KPIs for these objectives.*

GeoJSON is an open standard format designed for representing simple geographical features, along with their non-spatial attributes. It is based on JSON, the JavaScript Object Notation. The body of the specification deals with describing GeoJSON Geometry Objects. These may be points (which can be used for features like addresses and locations), line strings (e.g. for streets, highways, boundaries), polygons (countries, provinces, tracts of land), and multi-part collections of these types.

GeoJSON features need not represent entities of the physical world only; mobile routing and navigation apps, for example, might describe their service coverage using GeoJSON.

The GeoJSON format has originally been defined by an Internet working group of developers who needed a solution to encode geometries for use in web applications. It has since been formalised as an [IETF internet standard](https://tools.ietf.org/html/rfc7946). The IETF is the premier Internet standards organization.

A notable offspring of GeoJSON is [TopoJSON](https://github.com/topojson/topojson), an extension of GeoJSON that encodes geospatial topology and that provides smaller file sizes for polygons or other data sets where multiple features share geometries.

Within INSPIRE, this encoding represents an (TODO alternative|additional) encoding for data from several themes, with a focus on usability of the data in GIS desktop and web clients such as ArcMap, QGIS, OpenLayers, Leaflet, FME and hale studio.

## Scope

This sections describes the scope of the GeoJSON alternate encoding. GeoJSON is not equally well suited for all themes and use cases.

### Use Cases

This alternate encoding specifically addresses data usability in web and desktop client software, such as ArcMap, QGIS, Leaflet and OpenLayers. It optimizes usage of INSPIRE data for mapping and geoprocessing in such applications.

The encoding is also developed with the best practices for "Spatial data on the Web" and the WFS 3.0 standard in mind, for which it should provide a complementary format. 

TO DECIDE: What this encoding does not cover:

* 3D geometries
* Coverage/Raster data

### Coverage of INSPIRE Themes

This encoding covers the following themes:

TO DECIDE: which themes are covered?

### INSPIRE Requirements

The Implementing Rules on interoperability of spatial data sets and services (Commission Regulation (EU) No 1089/2010) lays down the following requirements for encodings:

> **Article 7 -- Encoding**
>
> 1. Every encoding rule used to encode spatial data shall conform to EN ISO 19118. In particular, it shall specify schema
> conversion rules for all spatial object types and all attributes and association roles and the output data structure used. 
> 2. Every encoding rule used to encode spatial data shall be made available.

D2.7 specifies more detailed requirements and recommendations for encodings. The following list lists the requirements from that document and shows which ones are also met in this alternate encoding:

> * Requirement 3: Every data specification that uses coverages shall specify how range values are encoded and how the information from the conceptual model is represented in the encoding so that a data provider can encode their coverage functions in a way that a receiving system can decode in an unambiguous way.
> * Requirement 6: Attributes and association roles with the stereotype <<voidable>> shall be converted to XML Schema as if the stereotype were ignored - except that the content model of the property element shall receive two additional optional attributes: 
>    * The global attribute `xsi:nil` (specified by XML Schema); in the schema this is expressed by an attribute `nillable` with the value `―true`. 
>    * A local, unqualified attribute ―nilReason with the type `gml:NilReasonType`.
> * Requirement 12: ... documents shall be required to be encoded using UTF-8 as character encoding.

D2.7 also lists several relevant recommendations:

* Recommendation 1: Every data specification should use the default encoding rule specified in Annex B as the mandatory encoding rule and document all additional type mappings.
* Recommendation 2: If the default encoding rule is not a mandatory encoding rule in a data specification, the reasons for this should be explained and the default encoding rule should be supported as an additional encoding rule.
* Recommendation 3: Encoding rules should be based on international, preferably open, standards.
* Recommendation 4: Additional encoding rules should only be added, if the new encoding rule has unique characteristics required by the data that are not fulfilled by an encoding rule that has already been endorsed.
* Recommendation 5: For the download of a pre-defined (part of a) spatial data set via the operations specified in part A of the download service implementing rule and for the download of spatial objects via the operations specified in part B of the download service implementing rule, the same object collection container should be used for the same type of representation.
* Recommendation 6: If the GetFeatureInfo operation is offered by a view service, it should use the same encoding as the download service.

## Normative References

This section contains references to standards documents and related resources.

* [GeoJSON - IETF RFC 7946](https://tools.ietf.org/html/rfc7946)

TODO: After definition of the INSPIRE themes for which this encoding will be applicble, add these references here.

## Terms and Definitions

A glossary of terms and their definitions used in the document.

TODO: Add Terms from issues and other sources as discussed in the WG

## General Encoding Rules

This section describes which common rules have to be applied for this encoding.

* `GEN-REQ-01`: The character encoding of all data encoding in GeoJSON shall be UTF-8.
* `GEN-REQ-02`: As per the requirements of the GeoJSON - IETF RFC 7946 specification, the default CRS for any data set delivered in this encoding shall be the World Geodetic System 1984 ([WGS 84](http://www.opengis.net/def/crs/OGC/1.3/CRS84)).

## Conformance Classes

This specification defines several conformance classes. The core GeoJSON class is optimized for usability in currently existing clients and describes how specifically to encode data sets for that prupose.

### Core GeoJSON support

#### Model Transformation

Any conformance class in an encoding specification may optionally define a number of model transformation rules that should be applied before the encoding. These transformations are documented in the [Best Practices for Model Transformations](../model-transformations/BestPracticesForModelTransformations.md) paper serve the purpose of adapting the conceptual model (UML) to better match the logical model of the target platform. In the context of this conformance class in the GeoJSON encoding, the described rules address the following issues:

* Multiple Geometries
* Nested Properties
* References to other elements and code lists
* Attributes such as `uom` and `nilReason`
* Arrays/Lists
* ...

#### Specific encoding rules for this conformance class

### Alternate Coordinate Reference System support

While the required Coordinate Reference System for any data encoded in GeoJSON is WGS84, a client may request delivery of a data set using a different projected reference system, as per the mechanism described in Requirement 8 in the [WFS 3.0 draft specification](https://github.com/opengeospatial/WFS_FES). 

* `PROJ-REQ-01`: An INSPIRE Download service delivering data encoded in GeoJSON shall be able to deliver projected geometries if a client requests these explicitly, at least for the spatial reference systems documented in section 6.3. of the data specifications that fall within the scope of this encodign specification.

### Array property support

High-cardinality properties can quickly lead to data usability issues when the property is simply flattened, as it can generate potentially hundreds of thousands of fields. Several of the clients as well as other delivery formats have limits on the number of supported fields, and using such data would become very unwieldy. At the same time, some clients such as QGIS support arrays of simple elements. This conformance clas thus allows arrays of simple properties to be used.


## Mapping from and to the Default INSPIRE encoding

TODO: Decide whether this is addressed by the descriptions of the model transformation rules.
TODO: Decide whether to provide an implementation-level mapping or a conceptual level mapping.

Describe how this data in this encoding can be derived from data encoded in INSPIRE GML.
Describe how data encoded in this alternate encoding can be transformed to INSPIRE GML.

## Annex I (Normative/Informative): Abstract / Executable Test Suite

Every alternative encoding needs to describe a method for validation of data sets using this encoding.

Describe how to ensure validity of a data set encoded using these rules. This description can be abstract or executable.
Examples:

* XML Schema
* JSON Schema
* ETS

## Annex II (Informative): Examples

Provide examples, at least one for each conformance class.
