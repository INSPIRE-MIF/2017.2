# GeoJSON Encoding Rule for INSPIRE Addresses

`Version: 0.1`
`Date: 2019-03-29`

The Simple Addresses encoding can be used as an *alternative encoding* for address data that fulfills the following requirements:

* It is sufficient to provide one `GeographicName` for all elements that use it 
* There is not more than 1 `AdminUnitName` address component per `AdministrativeUnitLevel`
* There is only a single default position per `Address` object

## Normative References

* [INSPIRE UML-to-GeoJSON encoding rule version 0.1](/GeoJSON/geojson-encoding-rule.md)
* [Data Specification - INSPIRE Addresses version 3.1](https://inspire.ec.europa.eu/Themes/79/2892)

## Conformance Class Core

The Addresses theme has one application schema, therefore this theme-specific encoding rule defines a single core conformance class.

### Model Transformation

This section describes which transformation rules with which parameters are applied to the Addresses conceptual model before applying the general rules of this encoding rule:

1. Substitute all occurences of `GeographicName` with the Simple Geographic Name through Rule `MT005(separator: '.')`. 
2. Subsitute all attributes that have a property type with a Codelist Sterotype through a inline codelist reference using `MT008()`.
3. Inline all `addressComponents` through Rule `MT003(separator: '.', cardinality: { AdminUnitName: 6 })`, using the respective typenames to create unique property names. In addition, define that for `AdminUnitName`, six properties shall be created, one for each `AdministrativeUnitLevel`.
4. Flatten the Locator/Designator structure through application of `MT004(separator: '.', keyProperty: 'type')` (Flatten aggregated or associated components using codelist values).
5. Apply the General Flattening rule to simplify the remaining properties: `MT001(separator: '.')`

### Model Mapping

The following table explains the mapping between the classes and properties of the original Addresses (AD) model to the Simplified Addresses (ADS) model.

#### Address

| AD Name (condition) | AD Type | ADS Name | ADS Type |
| ------------------- | ------- | -------- | -------- |
| ad:alternativeIdentifier | String | alternativeIdentifier | String |
| ad:beginLifespanVersion | DateTime | beginLifespanVersion | String |
| ad:endLifespanVersion | DateTime | endLifespanVersion | String |
| ad:building | bu-base:AbstractConstruction | building | String (URL) |
| ad:component (class = ThoroughfareName) | Component | component.ThoroughfareName | String |
| ad:component (class = PostalDescriptor) | Component | component.PostalDescriptor | String |
| ad:component (class = AddressAreaName) | Component | component.AddressAreaName | String |
| ad:component (class = AdminUnitName, index = 0) | Component | component.AdminUnitName_1 | String |
| ad:component (class = AdminUnitName, index = 1) | Component | component.AdminUnitName_2 | String |
| ad:component (class = AdminUnitName, index = 2) | Component | component.AdminUnitName_3 | String |
| ad:component (class = AdminUnitName, index = 3) | Component | component.AdminUnitName_4 | String |
| ad:component (class = AdminUnitName, index = 4) | Component | component.AdminUnitName_5 | String |
| ad:component (class = AdminUnitName, index = 5) | Component | component.AdminUnitName_6 | String |
| ad:locator | AddressLocator | locator.designator.addressNumber | String |
|  |  | locator.designator.addressNumberExtension | String |
|  |  | locator.designator.addressNumber2ndExtension | String |
|  |  | locator.designator.buildingIdentifier | String |
|  |  | locator.designator.buildingIdentifierPrefix | String |
|  |  | locator.designator.cornerAddress1stIdentifier | String |
|  |  | locator.designator.cornerAddress2ndIdentifier | String |
|  |  | locator.designator.entranceDoorIdentifier | String |
|  |  | locator.designator.floorIdentifier | String |
|  |  | locator.designator.kilometrePoint | String |
|  |  | locator.designator.postalDeliveryIdentifier | String |
|  |  | locator.designator.staircaseIdentifier | String |
|  |  | locator.designator.unitIdentifier | String |
|  |  | locator.level | String |
|  |  | locator.level.href | String (URL) |
| ad:parcel | Parcel | parcel | String |
| ad:parentAddress | Address | parentAddress | String |
| ad:position | GeographicPosition | *added as `geometry` to the root object* | GeoJSON Geometry Object |
|  |  | position.specification | String |
|  |  | position.specification.href | String (URL) |
|  |  | position.method | String |
|  |  | position.method.href | String (URL) |
|  |  | position.default | boolean |
| ad:status | StatusValue | status | String |
|  |  | status.href | String (URL) |
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
                "inspireId.localId": "Address_1",
                "inspireId.namespace": "https://github.com/INSPIRE-MIF/2017.2/GeoJSON/ads/examples/",
                "position.specification": "parcel",
                "position.specification.href": "http://inspire.ec.europa.eu/codelist/GeometrySpecificationValue/parcel",
                "position.method": "fromFeature",
                "position.method.href": "http://inspire.ec.europa.eu/codelist/GeometryMethodValue/fromFeature",
                "position.default": true,
                "locator.designator.addressNumber": "5",
                "locator.designator.addressNumberExtension": "A",
                "locator.level": "siteLevel",
                "locator.level.href": "http://inspire.ec.europa.eu/codelist/LocatorLevelValue/siteLevel",
                "component.ThoroughfareName": "Fraunhoferstraße",
                "component.PostalDescriptor": "64283",
                "component.AddressAreaName": "Innenstadt",
                "component.AdminUnitName_1": "Deutschland",
                "component.AdminUnitName_2": "Hessen",
                "component.AdminUnitName_3": "Darmstadt"
            }
        }
   ]
}
```

### JSON Schema Definition (Informative)
