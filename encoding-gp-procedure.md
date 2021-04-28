# Procedure for alternative encodings of INSPIRE data (DRAFT)

## Scope
This procedure describes the approach to be followed for encoding INSPIRE data in accordance with the Implementing Rules on interoperability of spatial data sets and services (IR ISDSS) through the use of alternative encodings, i.e. different from the default encoding - XML, but at the same time meeting all the legally-binding obligations of the IR ISDSS. 

Open Questions: are (i) additional encodings and (ii) extended INSPIRE models in scope? 

## Approach

### Principles
Adhereing to the following principles will facilitate the encoding of data under INSPIRE.

- A stepwise approach is envisioned for encoding the data. The steps to be followed are provided below.
- Should there be different proposals for the encoding of data for the same data model or data theme, the changes are discussed (i) between the proposers, ideally on GitHub, and if needed (ii) within the context of the temporary sub-group [2.3.1 'Governance of INSPIRE Artefacts'](https://webgate.ec.europa.eu/fpfis/wikis/display/InspireMIG/Action+2.3+Simplification+of+INSPIRE+implementation).

### Envisioned Steps

#### Step 1. Data encoding
Data should be encoded through the alternative encoding (e.g. GPKG or GeoJSON) by following the provisions of the INSPIRE UML models and/or Application schemas. When encoding the data the following should be consulted:
1. [Model transformation rules](https://github.com/INSPIRE-MIF/2017.2/blob/master/model-transformations/TransformationRules.md) that are encoding-agnostic, and
2. Encoding-specific rules  developed per each data encoding (e.g. for [GeoJSON](https://github.com/INSPIRE-MIF/2017.2/blob/master/GeoJSON/geojson-encoding-rule.md), GeoPackage, etc.)

#### Step 2. Describe the mapping to the default encoding
Once the data instances prepared in accordance with Step 1. are generated, mapping to the default INSPIRE encoding (XML) should be made available together with an example excerpt of a dataset on GitHub through at least one of the following means:
1. Executable transformation script, incl. software-specific approaches that can be replicated.
2. [INSPIRE Matching tables](https://inspire.ec.europa.eu/data-model/approved/r4618-ir/mapping/). Ideally, this should be done on the level of physical/format level, e.g. through mapping of xpaths versus jsonpaths, e.g.:

| GML        | GeoJSON           |
| ------------- |-------------|
| Ad:Address/inspireId/localId      | $.properties.inspireId_localId |
| Ad:Address/inspireId/namespace     | $.properties.inspireId_namespace     |
| ... | ...      |



#### Step 3. Data validation
Confirming the approach through the [INSPIRE reference validator](https://inspire.ec.europa.eu/validator/) can be achieved through deriving and validating GML instances based on the mapping performed in Step 2. The GML instances and the test report from the [INSPIRE reference validator](https://inspire.ec.europa.eu/validator/) (html) should be made available.
