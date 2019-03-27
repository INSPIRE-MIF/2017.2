## Restriction of property encoding options to only by-reference

<table>
<tr>
<td>Category</td>
<td>General model simplification rules</td>
</tr>
<tr>
<td>Description</td>
<td><p>Information regarding resources such as legal documents can be stored in an external register or non-INSPIRE online application, possibly using other standardised encodings.  Such information should not be duplicated in the INSPIRE model if possible. Thus, the information should be referred to from a GML application schema "by reference".</p>

<p>It gives a lot of work for data providers when they have to document a lot of metadata regarding e.g. laws, documents, authorities, etc. that they are not responsible for, and when this information is already online somewhere else this is redundant work. Therefore, properties referring to laws, documents, authorities and other online resources not typically belonging to the geographic information domain should be implemented by reference, and it should be recognised that their values are not necessarily encoded in a spatial data format.</p>
</td>
</tr>
<tr>
<td>UML Model</td>
<td>Not applicable (there is no single UML model that results from this transformation rule)</td>
</tr>
<tr>
<td>Original instance in default encoding:</td>
<td>
<p>Possibility 1: inline</p>

```xml
<am:ManagementRestrictionOrRegulationZone>
  <!-- ... -->
  <am:legalBasis>
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
      <base2:level
        xlink:href="http://inspire.ec.europa.eu/codelist/LegislationLevelValue/national"
        xlink:title="national" />
    </base2:LegislationCitation>
  </am:legalBasis>
  <!-- ... -->
</am:ManagementRestrictionOrRegulationZone>
```

<p>Possibility 2: by reference</p>

```xml
<am:ManagementRestrictionOrRegulationZone>
  <!-- ... -->
  <am:legalBasis
    xlink:href="http://www.retsinformation.dk/eli/lta/2017/122"
    xlink:title="Bekendtgørelse af lov om skove" />
  <!-- ... -->
</am:ManagementRestrictionOrRegulationZone>
```

<p>Possibility 3: by reference and inline. From the GML standard:</p>

<blockquote>If both a link and content are present in an instance of a property element, then the object found by traversing the xlink:href link shall be the normative value of the property. The object included as content shall be used by the data recipient only if the remote instance cannot be resolved; this may be considered to be a "cached" version of the object.</blockquote>

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
      <base2:level
        xlink:href="http://inspire.ec.europa.eu/codelist/LegislationLevelValue/national"
        xlink:title="national" />
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
<ams:ManagementRestrictionOrRegulationZone>
  <!-- ... -->
  <ams:legalBasis
    xlink:href="http://www.retsinformation.dk/eli/lta/2017/122"
    xlink:title="Bekendtgørelse af lov om skove"
  />
  <!-- ... -->
</ams:ManagementRestrictionOrRegulationZone>
```

</td>
</tr>
<tr>
<td>Model transformation rule: </td>
<td>
    <p>Parameters:</p>
    <ul>
        <li><code>referenceProperty</code>: The name of the property which to change to a reference.</li>
    </ul>
    <p>On the model level, this changes the tagged value <code>inlineOrByReference</code> to have the value <code>byReference</code> on the property.</p>
</td>
</tr>
<tr>
<td>Instance transformation rule:</td>
<td><p>Parameters: None</p>
    <p>It is only possible to convert an instance using the "inline" pattern when the URL is present in the original data or can be added upon transformation from the original data to the INSPIRE data. This URL must be inserted in <code>@xlink:href</code>. A name or title, if present, may be inserted in <code>@xlink:title</code>.</p>
    </td>
</tr>
<tr>
<td>Solves usability issues:</td>
<td>This rule reduces nested structures (inline referencing causes nested structures with many levels). It also reduces implementation effort of and duplication of data by data providers, if the value of the property is a resource managed by another data provider.</td>
</tr>
<tr>
<td>Known usability issues:</td>
<td>Display of <code>@xlink:href</code> and <code>@xlink:title</code> may not be supported in all clients. However, this is the same problem as for code lists, which are widely used in INSPIRE.</td>
</tr>
<tr>
<td>INSPIRE Compliance:</td>
<td>Fully compliant if the referenced resource is stored in an external register or non-INSPIRE online application.</td>
</tr>
<tr>
<td>Examples of this encoding rule:</td>
<td>TODO List issues in 2017.2 repo that have applied this pattern or very similar ones.</td>
</tr>
</table>

Notes: No notes.
