## Inline associated or aggregated components using type names

<table>
<tr>
<td>Category</td>
<td>General model simplification rules</td>
</tr>
<tr>
<td>Description</td>
<td><p>Several INSPIRE themes, such as Transport and Addresses, use Assocations to add a set of properties to a feature. An example for this is the `components` in `Address` in the `Addresses` theme. This property has a set of 1..n `AddressComponents` that together describe the actual address. In a simplified model, we want to replace this construct with a set of inlined properties. The individual components have a set of properties that make them unique - the `Type` of each property. We can thus use those Typenames to create a new set of properties from the original associated structures, like so:</p>
<ul>
    <li>component_ThoroughfareName</li>
    <li>component_PostalDescriptor</li>
    <li>component_AdminUnitName</li>
    <li>component_AddressAreaName</li>
</ul>
<p>This rule effectively denormalizes such associations. Please note the the individual properties such as `component_ThoroughfareName` are still complex; there is a need of additional rules to also simplify these.
</td>
</tr>
<tr>
<td>UML Model</td>
<td>TODO</td>
</tr>
<tr>
<td>Original instance in default encoding:</td>
<td>

```xml
<ad:Address gml:id="MIG20172_example_Address">
	<ad:inspireId>...</ad:inspireId>
	<ad:position>...</ad:position>
	<ad:locator>...</ad:locator>
	<ad:component xlink:href="#ThoroughfareName_1"/>
	<ad:component xlink:href="#AddressAreaName_1"/>
	<ad:component xlink:href="#PostalDescriptor_1"/>
</ad:Address>
...
<ad:ThoroughfareName gml:id="ThoroughfareName_1">
    <ad:inspireId>...</ad:inspireId>
    <ad:name>
        <ad:ThoroughfareNameValue>
            <ad:name>
                <GN:GeographicalName>
					<GN:language xsi:nil="true"/>
					...
					<GN:spelling>
						<GN:SpellingOfName>
							<GN:text>gn:language</GN:text>
						</GN:SpellingOfName>
					</GN:spelling>
					...
				</GN:GeographicalName>
            </ad:name>
        </ad:ThoroughfareNameValue>
    </ad:name>
</ad:ThoroughfareName>
<ad:AddressAreaName gml:id="AddressAreaName_1">
    <ad:inspireId>...</ad:inspireId>
    <ad:name>
        <gn:GeographicalName>
            <gn:language>ita</gn:language>
            ...
            <gn:spelling>
                <gn:SpellingOfName>
                    <gn:text>Ispra</gn:text>
                </gn:SpellingOfName>
            </gn:spelling>
            ...
        </gn:GeographicalName>
    </ad:name>
    <ad:namedPlace xsi:nil="true" nilReason="other:unpopulated"/>
</ad:AddressAreaName>
<ad:PostalDescriptor gml:id="PostalDescriptor_1">
    <ad:inspireId>...</ad:inspireId>
    <ad:postCode>21027</ad:postCode>
</ad:PostalDescriptor>
```
   
</td>
</tr>
<tr>
<td>Transformed instance in default encoding:</td>
<td>

```xml
<ad:Address gml:id="MIG20172_example_Address">
	<ad:inspireId>...</ad:inspireId>
	<ad:position>...</ad:position>
	<ad:locator>...</ad:locator>
	<ads:component_ThoroughfareName">
        <ad:ThoroughfareName gml:id="ThoroughfareName_1">
            <ad:inspireId>...</ad:inspireId>
            <ad:name>
                <ad:ThoroughfareNameValue>
                    <ad:name>
                        <GN:GeographicalName>
                            <GN:language xsi:nil="true"/>
                            ...
                            <GN:spelling>
                                <GN:SpellingOfName>
                                    <GN:text>gn:language</GN:text>
                                </GN:SpellingOfName>
                            </GN:spelling>
                            ...
                        </GN:GeographicalName>
                    </ad:name>
                </ad:ThoroughfareNameValue>
            </ad:name>
        </ad:ThoroughfareName>
    </ads:component_ThoroughfareName">
	<ads:component_AddressAreaName">
        <ad:AddressAreaName gml:id="AddressAreaName_1">
            <ad:inspireId>...</ad:inspireId>
            <ad:name>
                <gn:GeographicalName>
                    <gn:language>ita</gn:language>
                    ...
                    <gn:spelling>
                        <gn:SpellingOfName>
                            <gn:text>Ispra</gn:text>
                        </gn:SpellingOfName>
                    </gn:spelling>
                    ...
                </gn:GeographicalName>
            </ad:name>
            <ad:namedPlace xsi:nil="true" nilReason="other:unpopulated"/>
        </ad:AddressAreaName>
    </ads:component_AddressAreaName">
	<ads:component_PostalDescriptor">
        <ad:PostalDescriptor gml:id="PostalDescriptor_1">
            <ad:inspireId>...</ad:inspireId>
            <ad:postCode>21027</ad:postCode>
        </ad:PostalDescriptor>
    </ads:component_PostalDescriptor">
</ad:Address>

``` 

</td>
</tr>
<tr>
<td>Model transformation rule: </td>
<td>
    <p>Parameters: `separator`: The character to use to separate the original property name from the type name of the components.</p>
    <p>Create a new property for every possible associated type, using the original property name, the separator, and the name of the element (i.e. without a ...type suffix) to build the new property name.</p>
</td>
</tr>
<tr>
<td>Instance transformation rule:</td>
<td>For each potential type of a value, a property is created, so instance values can be copied. Properties that are left empty after copying the source values can be removed (see example above).</td>
</tr>
<tr>
<td>Solves usability issues:</td>
<td>Data where key properties are in associated objects is hard to style and to filter for in most desktop GIS and web GIS software. The inlined data can be processed much easier by many tools, e.g. it can be converted to excel easily</td>
</tr>
<tr>
<td>Known usability issues:</td>
<td>Since this rule denormalizes components, it can increase total data volume.</td>
</tr>
<tr>
<td>INSPIRE Compliance:</td>
<td>This rule can only be applied if there is at maximum one occurence of each type in a set of properties, i.e. where the components are a key-value map with the keys beign defined by the typenames.</td>
</tr>
<tr>
<td>Examples of this encoding rule:</td>
<td>TODO List issues in 2017.2 repo that have applied this pattern or very similiar ones.</td>
</tr>
</table>

Notes/Enhancements:

- We could expand this rule to allow higher cardinalities of the same type occuring using a postfix, e.g. `component_AddressAreaName_1` (or keep it simple)