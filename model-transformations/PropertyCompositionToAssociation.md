## Property Composition to Association

<table>
<tr>
<td>Category</td>
<td>General model simplification rules</td>
</tr>
<tr>
<td>Description</td>
<td><p>Information regarding resources such as legal documents can be stored in an external register or non-INSPIRE online application, possibly using other standardised encodings.  Such information should not be duplicated in the INSPIRE model if possible. THus, the information should be referred to from a GML application schema "by reference".</p>

<p>It gives a lot of work for data providers when they have to document a lot of metadata regarding e.g. laws, documents, authorities, etc. that they are not responsible for, and when this information is already online somewhere else this is redundant work. Therefore, properties referring to laws, documents, authorities and other online resources not typically belonging to the geographic information domain should be implemented by reference, and it should be recognised that their values are not necessarily encoded in GML.</p>
</td>
</tr>
<tr>
<td>UML Model</td>
<td>...</td>
</tr>
<tr>
<td>Original instance in default encoding:</td>
<td>

```xml
<am:ManagementRestrictionOrRegulationZone>
  <!-- ... -->
  <am:legalBasis
    xlink:href="http://www.retsinformation.dk/eli/lta/2017/122"
    xlink:title="Bekendtgørelse af lov om skove">
    <base2:LegislationCitation>
      <base2:name>Bekendtgørelse af lov om skove</base2:name>
      <base2:shortName>LBK nr 122 af 26/01/2017</base2:shortName>
      <base2:date>
        <gmd:CI_Date>
          <gmd:date>
            <gco:Date>2017-01-26</gco:Date>
          </gmd:date>
          <gmd:dateType>
            <gmd:CI_DateTypeCode
              codeListValue="creation"
              codeList="http://standards.iso.org/ittf/PubliclyAvailableStandards/ISO_19139_Schemas/resources/codelist/ML_gmxCodelists.xml#CI_DateTypeCode" />
          </gmd:dateType>
        </gmd:CI_Date>
      </base2:date>
      <base2:link>http://www.retsinformation.dk/eli/lta/2017/122</base2:link>
      <base2:level xlink:href="http://inspire.ec.europa.eu/codelist/LegislationLevelValue/national" xlink:title="national" />
    </base2:LegislationCitation>
  </am:legalBasis>
  <!-- ... -->
</am:ManagementRestrictionOrRegulationZone>
```
   
</td>
</tr>
<tr>
<td>Transformed instance in default encoding:</td>
<td>

```xml
<am:ManagementRestrictionOrRegulationZone>
  <!-- ... -->
  <am:legalBasis
    xlink:href="http://www.retsinformation.dk/eli/lta/2017/122"
    xlink:title="Bekendtgørelse af lov om skove"
  />
  <!-- ... -->
</am:ManagementRestrictionOrRegulationZone>
```

</td>
</tr>
<tr>
<td>Model transformation rule: </td>
<td>
    <p>Parameters:</p> 
    <ul>
        <li>`referenceProperty`: The name of the property which to change to a reference.</li>
    </ul>
    <p>On the model level, this changes the tagged value `inlineOrByReference` to have the value `byReference` on the property.</p>
</td>
</tr>
<tr>
<td>Instance transformation rule:</td>
<td><p>Parameters: None</p> 
    <p>It is only possible to convert an instance using the "inline" pattern when the URL is present somewhere in the data, which then must be inserted in `@xlink:href`. A name or title, if present, may be inserted in `@xlink:title`.</p>
    </td>
</tr>
<tr>
<td>Solves usability issues:</td>
<td>This rule reduces nested structures (inline referencing causes nested structures with many levels). It also reduces implementation effort of and duplication of data by data providers, if the value of the property is a resource managed by another data provider.</td>
</tr>
<tr>
<td>Known usability issues:</td>
<td>Display of `@xlink:href` and `@xlink:title` may not be supported in all clients. However, this is the same problem as for code lists, which are widely used in INSPIRE.</td>
</tr>
<tr>
<td>INSPIRE Compliance:</td>
<td>...</td>
</tr>
<tr>
<td>Examples of this encoding rule:</td>
<td>TODO List issues in 2017.2 repo that have applied this pattern or very similiar ones.</td>
</tr>
</table>

Notes: No notes.
