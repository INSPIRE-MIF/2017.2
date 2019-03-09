## Simplified Citation

<table>
<tr>
<td>Category</td>
<td>Alternate Structures for specific types or type hierarchies</td>
</tr>
<tr>
<td>Description</td>
<td><p>Citations are another element type that is used in many different places throughout the INSPIRE data specifications. There are concrete types such as `LegislationCitation`, which is an INSPIRE base type, but also types coming from other schemas, such as `CI_Citation` from ISO 19115. All of these structures tend to bury key information in deeply nested structures, creating a lot of overhead. This rule proposes a simplified altenrative representation.</p> 
<p>The simplified citation is based on a link to an external publication and adds minimal information with four properties:</p>
<ul>
    <li>citationDate</li>
	<li>citationLink</li>
	<li>citationName</li>
	<li>citationLevel</li>
	<li>citationType</li>
</ul>
<p>Each of these properties maps directly to an existing property of the original citation types. The `citationType` property can be used to indicate what kind of citation is represented by this object; its values can  be taken from the original type name, or can be base don a codelist.</p>
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
<gn:NamedPlace gml:id="MIG20172_example_NamedPlace">
	<gn:beginLifespanVersion xsi:nil="true"/>
	<gn:geometry>
		<gml:Point gml:id="_d7180a8f-a590-44da-8b45-41d96d5cba5e" srsName="http://www.opengis.net/def/crs/EPSG/0/25832" srsDimension="2">
		<gml:pos>471979.2568 5564594.2444</gml:pos>
		</gml:Point>
	</gn:geometry>
	<gn:inspireId>
		<base:Identifier>
			<base:localId>NamedPlace_Example</base:localId>
			<base:namespace>https://www.examples.eu/</base:namespace>
		</base:Identifier>
	</gn:inspireId>
	<gn:localType xsi:nil="true"/>
	<gn:name>
		<gn:GeographicalName>
			<gn:language>deu</gn:language>
			<gn:nativeness xsi:nil="true"/>
			<gn:nameStatus xsi:nil="true"/>
			<gn:sourceOfName xsi:nil="true"/>
			<gn:pronunciation xsi:nil="true"/>
			<gn:spelling>
				<gn:SpellingOfName>
				<gn:text>München</gn:text>
				<gn:script xsi:nil="true"/>
				</gn:SpellingOfName>
			</gn:spelling>
		</gn:GeographicalName>
	</gn:name>
	<gn:name>
		<gn:GeographicalName>
			<gn:language>eng</gn:language>
			<gn:nativeness xsi:nil="true"/>
			<gn:nameStatus xsi:nil="true"/>
			<gn:sourceOfName xsi:nil="true"/>
			<gn:pronunciation xsi:nil="true"/>
			<gn:spelling>
				<gn:SpellingOfName>
				<gn:text>Munich</gn:text>
				<gn:script xsi:nil="true"/>
				</gn:SpellingOfName>
			</gn:spelling>
		</gn:GeographicalName>
	</gn:name>
	<gn:type xsi:nil="true"/>
</gn:NamedPlace>
```
   
</td>
</tr>
<tr>
<td>Transformed instance in default encoding:</td>
<td>

```xml
<gns:NamedPlace gml:id="MIG20172_example_NamedPlace">
	<gns:beginLifespanVersion xsi:nil="true"/>
	<gns:geometry>
		<gml:Point gml:id="_d7180a8f-a590-44da-8b45-41d96d5cba5e" srsName="http://www.opengis.net/def/crs/EPSG/0/25832" srsDimension="2">
		<gml:pos>471979.2568 5564594.2444</gml:pos>
		</gml:Point>
	</gns:geometry>
	<gns:inspireId>
		<base:Identifier>
			<base:localId>NamedPlace_Example</base:localId>
			<base:namespace>https://www.examples.eu/</base:namespace>
		</base:Identifier>
	</gns:inspireId>
	<gns:localType xsi:nil="true"/>
	<gns:name_deu>München</gns:name_deu>
	<gns:name_eng>Munich</gns:name_eng>
	<gns:type xsi:nil="true"/>
</gns:NamedPlace>
``` 

</td>
</tr>
<tr>
<td>Model transformation rule: </td>
<td>
    <p>Parameters:</p> 
    <ul>
        <li>`separator`: The character to use to separate the original property name from the ISO 639-3 language code.</li>
		<li>`languageCodes`: A List of ISO 693-3 or ISO 693-5 codes for which to create the specific proeprties.</li>
    </ul>
    <p>Create a new property for every language given as a parameter. Give each property as name the concatenation of "name", the value of the separator parameter and the ISO 693-3 or ISO 693-5 code of the language.</p>
</td>
</tr>
<tr>
<td>Instance transformation rule:</td>
<td>
	<p>Copy the value of the `spelling.text` to the new property.</p>
</td>
</tr>
<tr>
<td>Solves usability issues:</td>
<td>The transformed data structure can easily be edited, filtered and symbolized in desktop GIS and web GIS software. This transformation also reduced data volume significantly in datasets that use in-place encoding of `GeographicalNames`.</td>
</tr>
<tr>
<td>Known usability issues:</td>
<td>None.</td>
</tr>
<tr>
<td>INSPIRE Compliance:</td>
<td>This rule discards individual metadata abour geographical names, such as the name status and its nativeness. If this information is homogeneous, it should be documented in the dataset metadata. If it is heterogeneous, this transformation will result in a loss of information and is not bijective.</td>
</tr>
<tr>
<td>Examples of this encoding rule:</td>
<td>TODO List issues in 2017.2 repo that have applied this pattern or very similiar ones.</td>
</tr>
</table>

Notes:

- This rule may be enhanced by storing additional properties that were present on the original name in "subfields" such as `name_deu_nativeness`.
