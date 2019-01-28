## Simplified Geographical Name

<table>
<tr>
<td>Category</td>
<td>Alternate Structures for specific types or type hierarchies</td>
</tr>
<tr>
<td>Description</td>
<td><p>Geographical Names are re-used throughout more than 20 INSPIRE themes overall, ranging from Cardastral Parcels and Addresses to Statistical Units. For many existing data sets, the `GeographicalName` type is overspecified, with very little information being unique to each instance. For cases</p>
<ul>
    <li>locator_designator_addressNumber</li>
    <li>locator_designator_addressNumberExtension</li>
    <li>locator_designator_entranceDoorIdentifier</li>
</ul>
<p>...</p>
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
	<ad:locator>
		<ad:AddressLocator>
			<ad:designator>
				<ad:LocatorDesignator>
					<ad:designator>99</ad:designator>
					<ad:type xlink:href="http://inspire.ec.europa.eu/codelist/LocatorDesignatorTypeValue/addressNumber">addressNumber</ad:type>
				</ad:LocatorDesignator>
			</ad:designator>
			<ad:level>unitLevel</ad:level>
		</ad:AddressLocator>
	</ad:locator>
	...
</ad:Address>
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
	<ads:locator_designator_addressNumber>99</ad:locator_designator_addressNumber>
	...
</ad:Address>
``` 

</td>
</tr>
<tr>
<td>Model transformation rule: </td>
<td>
    <p>Parameters:</p> 
    <ul>
        <li>`separator`: The character to use to separate the original property name from the type name of the components.</li>
    </ul>
    <p>Create a new property for every value in an associated code list, using the original property name, the separator, and the name of the element (i.e. without a ...type suffix) to build the new property name.</p>
</td>
</tr>
<tr>
<td>Instance transformation rule:</td>
<td><p>Parameters:</p> 
    <ul>
        <li>`valueProperty`: The name of the property from which to take the value to be copied to the transformed instance.</li>
    </ul>
    <p>Copy the value of the `valueProperty` to the newly created property. If the `valueProperty` is still a complex property, it might have to be transformed usign a different rule in addition.</p>
    </td>
</tr>
<tr>
<td>Solves usability issues:</td>
<td>The flattened data can be filtered and symbolized easily in desktop GIS and web GIS software. The flattened data can be processed much easier by many tools, e.g. it can be converted to excel easily</td>
</tr>
<tr>
<td>Known usability issues:</td>
<td>Flattening of large arrays will lead to a very large number of properties on the first level. Some software and formats can only work with a limited number of properties on a layer (ArcMap has 65.534, shapefile is limited to 250), so this can limit usability in extreme cases. Some software also has limits on the length of property names (File Geodatabase = 64 characters, Shapefile = 11 characters).</td>
</tr>
<tr>
<td>INSPIRE Compliance:</td>
<td>This rule can only be applied if there is at maximum one occurence of each codelist value for the type property in a set of properties.</td>
</tr>
<tr>
<td>Examples of this encoding rule:</td>
<td>TODO List issues in 2017.2 repo that have applied this pattern or very similiar ones.</td>
</tr>
</table>

Notes: No notes.
