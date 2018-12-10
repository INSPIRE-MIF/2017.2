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
    * Projected CRS support
    * Array property support
* Mapping to the Default INSPIRE encoding
    * This encoding to INSPIRE GML
	* INSPIRE GML to this encoding
* Annex I (Normative/Informative): Abstract / Executable Test Suite
* Annex II (Informative): Compatibility Tables 
* Annex III (Informative): Examples

## Introduction

*Describe what this document contains and what the high-level objective of this encoding is. Clarify the objectives, and ideally KPIs for these objectives.*

GeoJSON is an open standard format designed for representing simple geographical features, along with their non-spatial attributes. It is based on JSON, the JavaScript Object Notation.

The features include points (therefore addresses and locations), line strings (therefore streets, highways and boundaries), polygons (countries, provinces, tracts of land), and multi-part collections of these types. GeoJSON features need not represent entities of the physical world only; mobile routing and navigation apps, for example, might describe their service coverage using GeoJSON.

The GeoJSON has originally been defined by an Internet working group of developers who needed a solution to encode geometries for use in web applications. It has since been formalised as an [IETF internet standard](https://tools.ietf.org/html/rfc7946). The IETF is the premier Internet standards organization.

A notable offspring of GeoJSON is [TopoJSON](https://github.com/topojson/topojson), an extension of GeoJSON that encodes geospatial topology and that provides smaller file sizes for polygons or other data sets where multiple features share geometries.

Within INSPIRE, this encoding represents an (TODO alternative|additional) encoding for data from several themes, with a focus on usability of the data in GIS desktop and web clients such as ArcMap, QGIS, OpenLayers, Leaflet, FME and hale studio.

## Scope

This sections describes the scope of the GeoJSON alternate encoding. GeoJSON is not equally well suited for all themes and use cases.

### Use Cases

This alternate encoding specifically addresses data usability in web and desktop client software, such as ArcMap, QGIS, Leaflet and OpenLayers. It optimizes usage of INSPIRE data for mapping and geoprocessing in such applications.

The encoding is also developed with the best practices for "Spatial data on the Web" and the WFS 3.0 standard in mind, for which it should provide a complementary format. 

TO DECIDE: What this  encoding does not cover:

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

D2.7 specifies more detailed requirements and recommendations for encodings.

This encoding does not address all requirements laid out in the D2.7. The following list lists the requirements from that document and shows which ones are also met in this alternate encoding:

TO DECIDE: which requirements and recommendations should this encoding also meet?

* Requirement 1: Every encoding rule in INSPIRE shall conform to ISO 19118. In particular, it shall specify schema conversion rules for all elements of the conceptual schema language that are used in the INSPIRE application schemas to which the rule is applied.
* Requirement 2: Every data specification shall specify a mandatory encoding rule that has to be supported for the spatial data of that theme.
* Requirement 3: Every data specification that uses coverages shall specify how range values are encoded and how the information from the conceptual model is represented in the encoding so that a data provider can encode their coverage functions in a way that a receiving system can decode in an unambiguous way.
* Requirement 4: A GML application shall be specified for the application schema.
* Requirement 5: The encoding rule specified in ISO 19136 Annex E with the extensions in GML 3.3 shall be applied with the additional rules stated in this Annex. For types within the scope of the ISO/TS 19139 encoding rule, the encoding rule of ISO/TS 19139 shall be applied.
* Requirement 6: Attributes and association roles with the stereotype <<voidable>> shall be converted to XML Schema as if the stereotype were ignored - except that the content model of the property element shall receive two additional optional attributes: 
    * The global attribute `xsi:nil` (specified by XML Schema); in the schema this is expressed by an attribute `nillable` with the value `―true`. 
    * A local, unqualified attribute ―nilReason with the type `gml:NilReasonType`.
* Requirement 7: Not relevant
* Requirement 8: Not relevant
* Requirement 9: Not relevant
* Requirement 10: All INSPIRE code lists shall be assigned a tagged value "asDictionary" with the value "true".
* Requirement 11: Not relevant
* Requirement 12: XML documents shall be required to be encoded using UTF-8 as character encoding.
* Requirement 13: Not relevant

Recommendations from D2.7:

* Recommendation 1: Every data specification should use the default encoding rule specified in Annex B as the mandatory encoding rule and document all additional type mappings.
* Recommendation 2: If the default encoding rule is not a mandatory encoding rule in a data specification, the reasons for this should be explained and the default encoding rule should be supported as an additional encoding rule.
* Recommendation 3: Encoding rules should be based on international, preferably open, standards.
* Recommendation 4: Additional encoding rules should only be added, if the new encoding rule has unique characteristics required by the data that are not fulfilled by an encoding rule that has already been endorsed.
* Recommendation 5: For the download of a pre-defined (part of a) spatial data set via the operations specified in part A of the download service implementing rule and for the download of spatial objects via the operations specified in part B of the download service implementing rule, the same object collection container should be used for the same type of representation.
* Recommendation 6: If the GetFeatureInfo operation is offered by a view service, it should use the same encoding as the download service.

## Normative References

This section contains references to standards documents and related resources:

* [GeoJSON - IETF RFC 7946](https://tools.ietf.org/html/rfc7946)

## Terms and Definitions

A glossary of terms and their definitions used in the document.

## General Encoding Rules

Required section. Describes the common rules of the encoding.

* Character Encoding in UTF-8
* Default CRS is WGS 84

## Conformance Classes

Optional section, required only if the specification defines conformance classes. If it does, this seection should always start with a "core" conformance class. It can then add any number of additional conformance classes.

## Mapping to the Default INSPIRE encoding

Decide whether to provide an implementaiton-level mapping or a conceptual level mapping.
Describe how this encoding can be derived from data encoded in INSPIRE GML.
Describe how data encoded in this alternate encoding can be transformed to INSPIRE GML.

## Annex I (Normative/Informative): Abstract / Executable Test Suite

Every alternative encoding needs to describe a method for validation of data sets using this encoding.

Describe how to ensure validity of a data set encoded using these rules. This description can be abstract or executable.
Examples:

* XML Schema
* JSON Schema
* ETS
* OpenAPI

## Annex II (Informative): Compatibility Tables 

Show which conformance classes can be used with which software (“Can I Use…”)

## Annex III (Informative): Examples

Provide examples, at least one for each conformance class.
