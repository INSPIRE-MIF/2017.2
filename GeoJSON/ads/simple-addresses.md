# GeoJSON Encoding Rule for INSPIRE Addresses

`Version: 0.2`
`Date: 2019-08-31`

The Simple Addresses encoding can be used as an *alternative encoding* for address data that fulfills the following requirements:

* It is sufficient to provide one `GeographicName` for all elements that use it 
* There is not more than 1 `AdminUnitName` address component per `AdministrativeUnitLevel`
* There is only a single default position per `Address` object

## Normative References

* [INSPIRE UML-to-GeoJSON encoding rule version 0.2](/GeoJSON/geojson-encoding-rule.md)
* [Data Specification - INSPIRE Addresses version 3.1](https://inspire.ec.europa.eu/Themes/79/2892)

## Conformance Class Core

The Addresses theme has one application schema, therefore this theme-specific encoding rule defines a single core conformance class.

### Model Transformation

This section describes which transformation rules with which parameters are applied to the Addresses conceptual model before applying the general rules of this encoding rule:

1. Substitute all occurences of `GeographicName` with the Simple Geographic Name through Rule `MT005(separator: '_')`. 
2. Subsitute all attributes that have a property type with a Codelist Sterotype through a inline codelist reference using `MT008()`.
3. Inline all `addressComponents` through Rule `MT003(separator: '_', cardinality: { AdminUnitName: 6 })`, using the respective typenames to create unique property names. In addition, define that for `AdminUnitName`, six properties shall be created, one for each `AdministrativeUnitLevel`.
4. Flatten the Locator/Designator structure through application of `MT004(separator: '_', keyProperty: 'type')` (Flatten aggregated or associated components using codelist values).
5. Apply the General Flattening rule to simplify the remaining properties: `MT001(separator: '_')`

### Model Mapping

The following table explains the mapping between the classes and properties of the original Addresses (AD) model to the Simplified Addresses (ADS) model.

#### Address

| AD Name (condition) | AD Type | ADS Name | ADS Type |
| ------------------- | ------- | -------- | -------- |
| ad:alternativeIdentifier | String | alternativeIdentifier | String |
| ad:beginLifespanVersion | DateTime | beginLifespanVersion | String |
| ad:endLifespanVersion | DateTime | endLifespanVersion | String |
| ad:building | bu-base:AbstractConstruction | building | String (URL) |
| ad:component (class = ThoroughfareName) | Component | component_ThoroughfareName | String |
| ad:component (class = PostalDescriptor) | Component | component_PostalDescriptor | String |
| ad:component (class = AddressAreaName) | Component | component_AddressAreaName | String |
| ad:component (class = AdminUnitName, index = 0) | Component | component_AdminUnitName_1 | String |
| ad:component (class = AdminUnitName, index = 1) | Component | component_AdminUnitName_2 | String |
| ad:component (class = AdminUnitName, index = 2) | Component | component_AdminUnitName_3 | String |
| ad:component (class = AdminUnitName, index = 3) | Component | component_AdminUnitName_4 | String |
| ad:component (class = AdminUnitName, index = 4) | Component | component_AdminUnitName_5 | String |
| ad:component (class = AdminUnitName, index = 5) | Component | component_AdminUnitName_6 | String |
| ad:locator | AddressLocator | locator_designator_addressNumber | String |
|  |  | locator_designator_addressNumberExtension | String |
|  |  | locator_designator_addressNumber2ndExtension | String |
|  |  | locator_designator_buildingIdentifier | String |
|  |  | locator_designator_buildingIdentifierPrefix | String |
|  |  | locator_designator_cornerAddress1stIdentifier | String |
|  |  | locator_designator_cornerAddress2ndIdentifier | String |
|  |  | locator_designator_entranceDoorIdentifier | String |
|  |  | locator_designator_floorIdentifier | String |
|  |  | locator_designator_kilometrePoint | String |
|  |  | locator_designator_postalDeliveryIdentifier | String |
|  |  | locator_designator_staircaseIdentifier | String |
|  |  | locator_designator_unitIdentifier | String |
|  |  | locator_name | SimpleGeographicName |
|  |  | locator_level | String |
|  |  | locator_level_href | String (URL) |
| ad:parcel | Parcel | parcel | String |
| ad:parentAddress | Address | parentAddress | String |
| ad:position | GeographicPosition | *added as `geometry` to the root object* | GeoJSON Geometry Object |
|  |  | position_specification | String |
|  |  | position_specification_href | String (URL) |
|  |  | position_method | String |
|  |  | position_method_href | String (URL) |
|  |  | position_default | boolean |
| ad:status | StatusValue | status | String |
|  |  | status_href | String (URL) |
| ad:validFrom | DateTime | validFrom | String |
| ad:validTo | DateTime | validTo | String |

### Examples (Informative)

NOTE Additional examples can be added to the [`/ads/examples/`](/GeoJSON/ads/examples/) folder in this repository.

**Example 1:** One Address Feature with all components and locators inlined ([Standalone Example](./examples/ads_example_1.geojson))

```json
{  
   "type":"FeatureCollection",
   "features":[ 
        {
            "type": "Feature",
            "id": "Address_1",
            "geometry": {
                "type": "Point",
                "coordinates": [ 8.6572813, 49.87437 ]
            },
            "properties": {
                "inspireId_localId": "Address_1",
                "inspireId_namespace": "https://github.com/INSPIRE-MIF/2017.2/GeoJSON/ads/examples/",
                "position_specification": "parcel",
                "position_specification.href": "http://inspire.ec.europa.eu/codelist/GeometrySpecificationValue/parcel",
                "position_method": "fromFeature",
                "position_method_href": "http://inspire.ec.europa.eu/codelist/GeometryMethodValue/fromFeature",
                "position_default": true,
                "locator_designator_addressNumber": "5",
                "locator_designator_addressNumberExtension": "A",
                "locator_level": "siteLevel",
                "locator_level_href": "http://inspire.ec.europa.eu/codelist/LocatorLevelValue/siteLevel",
                "locator_name": "Fraunhofer IGD",
                "component_ThoroughfareName": "Fraunhoferstraße",
                "component_PostalDescriptor": "64283",
                "component_AddressAreaName": "Innenstadt",
                "component_AdminUnitName_1": "Deutschland",
                "component_AdminUnitName_2": "Hessen",
                "component_AdminUnitName_3": "Darmstadt"
            }
        }
   ]
}
```

### JSON Schema Definition (Informative)
