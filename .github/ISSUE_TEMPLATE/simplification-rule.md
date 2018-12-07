---
name: Simplification Rule
about: This issue documents a single simplification rule

---

**Simplification Model Transformation Rule**

This rule issue is to be referenced from the best practive paper.

Use the sections below to specify the Model Transformation rule.

## Name of the Rule

Give the rule a summary name.

## Category

Add the category into one of the following categoies:

* Alternate Structures for specific types or type hierarchies (can be applied to specific types)
* General model simplification rules (can be applied everywhere)
* Flatten nested structures
* Flatten attributes (e.g. uom)
* Flatten lists/arrays
* Profiling (reduction of degrees of freedom, e.g. usage of property types in choices)

## Description

Prosa description of the purpose and approach of the transformation rule.

## UML Model

If this rule falls into the "Alternate Structures for specific types" category, provide a UML class diagram of your alternative model. For other rules, you may optionally provide a UML diagram.

## Example instance in default encoding:

Provide an example in the default encoding.

## Example instance in simplified encoding:

Provide an example feature that is based on the transformed model. 

## Model transformation rule:

Describe the actual model transformation rule, either in free text or in an algorithmic form.

## Instance transformation rule:

Describe how data in a property needs to be transformed, if necessary. As an example, there are rules which concatenate values (e.g. in the GeoSciML Lite approach).

## Solves usability issues:

Describe as concrete as possible, ideally using the test classes described in [CanIUse](), which issues in which software this approach addresses and solves.

## Known usability issues:

Describe whether this transformation leaves problems unsolved, or introduces new issues.

## Reversibility:

Describe whether the transformation is unidirectional from the default model / encoding to the simplified model / encoding, or whether it can be partially or entirely reversed.

