# Template for Alternate Encodings for INSPIRE Data

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
    * Core
    * 3D
    * Coverage
    * ...
* Mapping to the Default INSPIRE encoding
    * This encoding to INSPIRE GML
	* INSPIRE GML to this encoding
* Annex I (Normative/Informative): Abstract / Executable Test Suite
* Annex II (Informative): Compatibility Tables 
* Annex III (Informative): Examples

## Introduction

Describe what this document contains and what the high-level objective of this encoding is.

## Scope

Describe the scope of this alternate encoding in terms of...:

* Use Cases (generic or domain-specific use cases in which INSPIRE data become significantly more useable through this encoding)
* Coverage of INSPIRE Themes (at minimum, one)
* Cross-cutting INSPIRE requirements (general INSPIRE requirements that are addressed by this encoding)

## Normative References

References to standards documents and related resources.

## Terms and Definitions

A glossary of terms and their definitions used in the document.

## General Encoding Rules

Required section. Describes the common rules of the encoding.

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