# GeoJSON Encoding Rule for INSPIRE Environmental Monitoring Facilities

`Version: 0.1`
`Date: 2019-03-29`

Environmental Monitoring Facilities describe measuring stations, networks and programs, and makes use of Observations & Measurement (`OM`) data, in many cases using specific observations (`OMSO`).

The purpose of the this encoding rule is to create a simple structure for the data directly related to the monitoring facility itself so that users can create simple maps with info on measurements station with the actual measures inlined. A typical feature will thus describe *one* monitoring facility with one measurement result for one given point in time. Since information about the point in time and the result are inlined, tools such as ArcGIS can use this information with the inbuilt time series visualisation tools as well.

An additional objective is to provide an efficient structure for the measurements made by a monitoring facility. This is achieved by building on the rules defined in the `OMSF GeoJSON` encoding.

This encoding rule can be used as an *alternative encoding* for Environmental Monitoring Facility data that fulfills the following requirements:

* Only one legal background document needs to be referenced
* The measurements are of the following types: Simple result, `PointObservation`, `PointTimeSeriesObservation`, `MultiPointObservation`, `ProfileObservation` or `TrajectoryObservation` 

## Normative References

* [Data Specification - INSPIRE Environmental Monitoring Facilities version 3.0](https://inspire.ec.europa.eu/Themes/120/2892)
* [OGC Observations and Measurements - Simple Feature model & encodings (OMSF)](https://github.com/opengeospatial/omsf-profile)
* [OGC Observations and Measurements - Simple Feature GeoJSON Encoding (OMSF GeoJSON)](https://github.com/opengeospatial/omsf-profile/tree/master/omsf-json)

## Conformance Class Core

The Environmental Monitoring Facilities theme has one application schema, therefore this theme-specific encoding rule defines a single core conformance class.

### Model Transformation

This section describes which rules with which parameters are applied to the Environmental Monitoring Facilities conceptual model before applying the general rules of this encoding:

1. Substitute all occurences of `LegalCitation` with the Simple Citation through Rule `MT007()`.
2. Apply `MT006()` to add optional external information about citations.
3. Substitute all attributes that have a property type with a Codelist Sterotype through a simple codelist reference using `MT008()`.
4. Substitute `OperationalActivityPeriod` with the Simple Period using `MT009()`.
5. Substitute all `OM` and `OMSO` model elements through the respective `OMSF` model elements.
6. Apply the `OMSF GeoJSON` model mapping to the `OMSO` model elements.
7. Apply the General Flattening rule to simplify the remaining properties: `MT001(separator: '.')`.

### Model Mapping

### Examples (Informative)

**Example 1:** One Environmental Monitoring Facility with a single measurement result ([Standalone Example](./examples/example_1.geojson))

```json
{  
   "type":"FeatureCollection",
   "features":[ 
        {
            "type": "Feature",
            "id": "EnvironmentalMonitoringFacility_1",
            "geometry": {
                "type": "Point",
                "coordinates": [ 5.18713, 46.19095 ]
            },
            "properties": {
                "description": "Water well from national BSS (Banque du Sous-Sol) Data database. Piezometer monitoring ground water level",
                "inspireId.localId": "EnvironmentalMonitoringFacility_1",
                "inspireId.namespace": "https://github.com/INSPIRE-MIF/2017.2/GeoJSON/ems/examples/",
                "identifier": "https://github.com/INSPIRE-MIF/2017.2/GeoJSON/ems/examples/EnvironmentalMonitoringFacility_1",
                "legalBackground.date": "1977-10-08T23:00:00Z",
                "legalBackground.link": "",
                "legalBackground.name": "",
                "legalBackground.level": "",
                "legalBackground.level.href": "",
                "legalBackground.type": "",
                "mediaMonitored": "water",
                "mediaMonitored.href": "http://inspire.ec.europa.eu/codelist/MediaValue/water",
                "mobile": false,
                "name": "Piézomètre de St-Rémy - 01",
                "observation.resultTime": "2017-08-17T12:11:20Z",
                "observation.result": 220.58,
                "observation.unitOfMeasureName": "meter",
                "onlineResource": "http://fichebsseau.brgm.fr/bss_eau/fiche.jsf?code=06512X0037/STREMY",
                "operationalActivityPeriod.beginPosition": "1977-10-08T23:00:00Z",
                "operationalActivityPeriod.endPosition": "2014-10-14T06:00:00Z",
                "purpose": "Ground water level measurement",
                "purpose.href": "http://www.sandre.eaufrance.fr/?urn=urn:sandre:donnees:148::CdElement:2:::referentiel:3.1:xml",
                "resultAcquisitionSource": "in-situ",
                "resultAcquisitionSource.href": "http://inspire.ec.europa.eu/codelist/ResultAcquisitionSourceValue/inSitu/",
                "specialisedEMFType": "Piezometre",
                "specialisedEMFType.href": "http://www.sandre.eaufrance.fr/urn.php?urn=urn:sandre:dictionnaire:PTE::entite:Piezometre:ressource:2.1:::html"
            }
        }
   ]
}
```

**Example 2:** One Environmental Monitoring Facility with a reference to a `PointTimeSeriesObservation` ([Standalone Example](./examples/example_2.geojson))

```json
{  
   "type":"FeatureCollection",
   "features":[
       {
            "type": "Feature",
            "id": "EnvironmentalMonitoringFacility_1",
            "geometry": {
                "type": "Point",
                "coordinates": [ 5.18713, 46.19095 ]
            },
            "properties": {
                "description": "Water well from national BSS (Banque du Sous-Sol) Data database. Piezometer monitoring ground water level",
                "inspireId.localId": "EnvironmentalMonitoringFacility_1",
                "inspireId.namespace": "https://https://github.com/INSPIRE-MIF/2017.2/GeoJSON/examples/ems/",
                "identifier": "https://https://github.com/INSPIRE-MIF/2017.2/GeoJSON/examples/ems/EnvironmentalMonitoringFacility_1",
                "mediaMonitored": "water",
                "mediaMonitored.href": "http://inspire.ec.europa.eu/codelist/MediaValue/water",
                "name": "Piézomètre de St-Rémy - 01",
                "hasObservation.href": "#MeasureTimeseriesObservation_1",
                "onlineResource": "http://fichebsseau.brgm.fr/bss_eau/fiche.jsf?code=06512X0037/STREMY",
                "operationalActivityPeriod.beginPosition": "1977-10-08T23:00:00Z",
                "operationalActivityPeriod.endPosition": "2014-10-14T06:00:00Z",
                "purpose": "Ground water level measurement",
                "purpose.href": "http://www.sandre.eaufrance.fr/?urn=urn:sandre:donnees:148::CdElement:2:::referentiel:3.1:xml",
                "resultAcquisitionSource": "in-situ",
                "resultAcquisitionSource.href": "http://inspire.ec.europa.eu/codelist/ResultAcquisitionSourceValue/inSitu/",
                "specialisedEMFType": "Piezometre",
                "specialisedEMFType.href": "http://www.sandre.eaufrance.fr/urn.php?urn=urn:sandre:dictionnaire:PTE::entite:Piezometre:ressource:2.1:::html"
            }
        },
        {
            "type": "Feature",
            "id": "PointTimeSeriesObservation_1",
            "geometry": {
                "type": "Point",
                "coordinates": [ 5.18713, 46.19095 ]
            },
            "properties": {
                "observationType": "PointTimeSeriesObservation",
                "phenomenonTimeStart": "2015-11-07T12:00:00Z",
                "phenomenonTimeEnd": "2015-12-19T12:00:00Z",
                "resultTime": "2015-12-19T12:11:20Z",
                "usedProcedureName": "",
                "usedProcedureReference": "",
                "observedPropertyName": "",
                "observedPropertyReference": "",
                "samplingFeatureName": "Piézomètre de St-Rémy - 01",
                "ultimateFeatureOfInterestName": "",
                "ultimateFeatureOfInterestReference": "",
                "timeStep": [
                    "2015-11-07T12:00:00Z",
                    "2015-11-14T12:00:00Z",
                    "2015-11-21T12:00:00Z",
                    "2015-11-28T12:00:00Z",
                    "2015-12-05T12:00:00Z",
                    "2015-12-12T12:00:00Z",
                    "2015-12-19T12:00:00Z"
                ],
                "unitOfMeasureName": "meter",
                "unitOfMeasureReference": "http://www.opengis.net/def/uom/UCUM/m",
                "result": [220.91, 220.78, 220.54, 220.61, 220.28, 220.12, 220.20]
            }
        }
   ]
}
```

### JSON Schema Definition (Informative)