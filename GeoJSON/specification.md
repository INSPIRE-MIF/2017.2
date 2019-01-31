# Alternate Encoding for INSPIRE Data: GeoJSON

## Table of Contents

* Introduction
* Scope
    * Use Cases
	* Themes
    * Technical Issues
	* Cross-cutting INSPIRE requirements
* Normative References
* Terms and Definitions
* General Encoding rules
    * Requirements and Recommendations
    * Alternate Coordinate Reference Systems
* Conformance Classes
    * Simple Addresses
    * Simple Environmental Monitoring Facilities
* Annex I (Normative/Informative): Abstract / Executable Test Suite
* Annex II (Informative): Examples

## Introduction

This section describes what this document contains and what the high-level objective of this encoding is.

GeoJSON is an open standard format designed for representing simple geographical features, along with their non-spatial attributes. It is based on JSON, the JavaScript Object Notation. The body of the specification deals with describing GeoJSON Geometry Objects. These may be points (which can be used for features like addresses and locations), line strings (e.g. for streets, highways, boundaries), polygons (countries, provinces, tracts of land), and multi-part collections of these types.

GeoJSON features need not represent entities of the physical world only; mobile routing and navigation apps, for example, might describe their service coverage using GeoJSON.

The GeoJSON format has originally been defined by an Internet working group of developers who needed a solution to encode geometries for use in web applications. It has since been formalised as an [IETF internet standard](https://tools.ietf.org/html/rfc7946). The IETF is the premier Internet standards organization.

A notable offspring of GeoJSON is [TopoJSON](https://github.com/topojson/topojson), an extension of GeoJSON that encodes geospatial topology and that provides smaller file sizes for polygons or other data sets where multiple features share geometries.

Within INSPIRE, this encoding represents an *alternative* encoding for data from several themes, with a focus on usability of the data in GIS desktop and web clients such as ArcMap, QGIS, OpenLayers, Leaflet, FME and hale studio. It can server as an alternative encoding that can be used instead of the default encoding for simple data, where there is no information loss. In other cases, this GeoJSON encoding may serve as an *additional* encoding only.

This draft Alternative Encoding encompasses the INSPIRE themes Addresses (including GeographicalName properties) and Environmental Monitoring Facilities (including O&M properties).

## Scope

This sections describes the scope of the GeoJSON alternate encoding. GeoJSON is not equally well suited for all themes and use cases.

### Use Cases

This alternate encoding specifically addresses data usability in web and desktop client software, such as ArcMap, QGIS, Leaflet and OpenLayers. It optimizes usage of INSPIRE data for mapping and geoprocessing in such applications.

The encoding is also developed with the best practices for [Spatial data on the Web](https://www.w3.org/TR/sdw-bp/) and the [WFS 3.0 standard](https://github.com/opengeospatial/WFS_FES) in mind, for which it should provide a complementary format. 

The encoding does not cover:

* 3D geometries
* Coverage/Raster data

### Coverage of INSPIRE Themes

This encoding covers the following themes:

* Annex I: Addresses
* Annex III: Environmental Monitoring Facilities

### Technical Issues

The encoding resolves specific technical issues that have been problematic when using the default encoding:

* TODO List specific issues (see findings in https://github.com/INSPIRE-MIF/2017.2/issues/48)
* TODO List specific issues related to ArcGIS (see https://github.com/INSPIRE-MIF/2017.2/issues/18)
* Abstract geometry types for an object (mixed geometry types in a FeatureCollection)
* Be able to display types on map, e.g. date/time, xlinks, coded values and codelists

### INSPIRE Requirements for Encodings

The Implementing Rules on interoperability of spatial data sets and services (Commission Regulation (EU) No 1089/2010) lays down the following requirements for encodings:

> **Article 7 -- Encoding**
>
> 1. Every encoding rule used to encode spatial data shall conform to EN ISO 19118. In particular, it shall specify schema
> conversion rules for all spatial object types and all attributes and association roles and the output data structure used. 
> 2. Every encoding rule used to encode spatial data shall be made available.

D2.7 specifies more detailed requirements and recommendations for encodings. The following list lists the requirements from that document and shows which ones are also met in this alternate encoding:

> * Requirement 12: ... documents shall be required to be encoded using UTF-8 as character encoding.

D2.7 also lists several relevant recommendations:

* Recommendation 3: Encoding rules should be based on international, preferably open, standards.

## Normative References

This section contains references to standards documents and related resources.

* [GeoJSON - IETF RFC 7946](https://tools.ietf.org/html/rfc7946)
* INSPIRE Addresses
* INSPIRE Environmental Monitoring Facilities

## Terms and Definitions

A glossary of terms and their definitions used in the document.

TODO: Add Terms from issues and other sources as discussed in the WG

## General Encoding Rules

This section describes which common rules have to be applied for this encoding.

* `GEOJSON-REQ-01`: The character encoding of all data encoding in GeoJSON shall be UTF-8.
* `GEOJSON-REQ-02`: As per the requirements of the GeoJSON - IETF RFC 7946 specification, the default CRS for any data set delivered in this encoding shall be the World Geodetic System 1984 ([CRS 84](http://www.opengis.net/def/crs/OGC/1.3/CRS84)), unless there is prior arrangement.

NOTE As INSPIRE mandates the use of the European Terrestrial Reference System 1989  (ETRS89, see [Requirement 1](https://inspire.ec.europa.eu/reports/ImplementingRules/DataSpecifications/INSPIRE_Specification_CRS_v2.0.pdf)) for the areas within the geographical scope of ETRS89 and both CRS84 and ETRS89 use the GRS 80 ellipsoid (although with minor enhancements), we shall assume CRS 84 to be equivalent to ETRS89. If, for any dataset, this assumption would be problematic, then GeoJSON cannot serve as an alternative encoding for that dataset.

* `GEOJSON-REQ-03`: In the GeoJSON encoding, `nilReason` information shall not be maintained per feature, but rather in the dataset metadata. Properties that have `nil` values shall thus be ignored in the encoding.

NOTE If, for any dataset, there is specific `nilReason` information per feature, then GeoJSON cannot serve as an alternative encoding for that dataset

### Alternate Coordinate Reference System support

While the required Coordinate Reference System for any data encoded in GeoJSON is CRS84, a client may request delivery of a data set using a different projected reference system, as per the mechanism described in Requirement 8 in the [WFS 3.0 draft specification](https://github.com/opengeospatial/WFS_FES). 

* `GEOJSON-REC-01`: An INSPIRE Download service delivering data encoded in GeoJSON shall be able to deliver projected geometries if a client requests these explicitly, at least for the spatial reference systems documented in section 6.3. of the data specifications that fall within the scope of this encodign specification. When delivering data that is not in [CRS 84](http://www.opengis.net/def/crs/OGC/1.3/CRS84), the GeoJSON data should include the `crs` member as defined in the deprecated (Draft 6 of the GeoJSON specification)[http://wiki.geojson.org/GeoJSON_draft_version_6].

## Conformance Classes

This specification defines one conformance class per supported theme. 

Any conformance class in an encoding specification may  define a number of model transformation rules that should be applied before the encoding. These transformations are documented in the [Model Transformation Rules](../model-transformations/TransformationRules.md) paper. They serve the purpose of adapting the conceptual model (UML) to better match the logical model of the target platform. In the context of this conformance class in the GeoJSON encoding, the described rules address the following issues:

* Multiple Geometries
* Nested Properties
* References to other elements and code lists
* Attributes such as `uom` and `nilReason`
* Arrays/Lists

### Simple Addresses (ads)

#### Model Transformation

This section describes which rules with which parameters are applied to the Addresses conceptual model before applying the general rules of this encoding:

1. Substitute all occurences of GeographicName with the Simple Geographic Name through Rule `MT005(separator: '_')`. 
2. Inline all addressComponents through Rule `MT003(separator: '_')`, using the respective typenames to create unique property names.
3. Flatten the Locator/Designator structure through application of `MT004(separator: '_', keyProperty: 'type')` (Flatten aggregated or associated components using codelist values).
4. Apply the General Flattening rule to simplify the remaining properties: `MT003(separator: '_')`

#### Abstract Test Suite

TODO

#### Examples

TODO

### Simple Environmental Monitoring Facilities (ems)



