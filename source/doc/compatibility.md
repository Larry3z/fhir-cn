title: 
date: 
categories: doc
---

## <span class="sectioncount">?.?<a name="?.?"> </a></span> Inter-version Compatibility

<a name="version"> </a>

## <span class="sectioncount">?.?<a name="?.?"> </a></span> Inter-version Compatibility

> The following rules will apply to resources, profiles and other content within the specification
> once those portions of the specification reach [full normative status](timeline.html#normative).
> These rules ensure that implementations may exercise FHIR interfaces and process the content 
> of FHIR resources safely while exchanging data between applications using different
> versions of FHIR.
> 
> During the period of trial use of the specification (and once normative status is reached for elements that
> remain at draft or trial use status), changes may occur based on issues identified during early implementation of the 
> specification.  These changes do not need to adhere to the rules listed below.

### <span class="sectioncount">?.?.1<a name="?.?.1"> </a></span> Version identification

There is no explicit version marker in the resource content.  FHIR adheres to the DICOM approach to versioning where
content can safely be processed by instances independent of version.  When dealing with
DSTU-level content, applications may wish to use [resource tags](resource.html#tags) to help
manage this during the period of trial use.

The conformance layer ([Conformance](conformance.html) and [Profile](profile.html))
has mandatory properties declaring the FHIR specification version, and these may be used to determine
which version of FHIR an implementation is using to aid in validation.

### <span class="sectioncount">?.?.2<a name="?.?.2"> </a></span> Change frequency

New versions of the FHIR specification will be produced regularly in accordance with the 
[FHIR publication timeline](timelines.html).  New versions of the specification will include
additional draft and trial use content as well as promotion of previous trial use content to normative.
Once content reaches normative, changes are expected to be infrequent.  This is for two reasons:

1.  The core specification focuses on those capabilities expected to be supported by most systems.  For
  new capabilities to be introduced, it would need to be reflective of an overall change in the world-wide
  healthcare implementation environment.
2.  If the implementation community has already consolidated around a standard approach to solving a
  FHIR implementation issue (e.g. using a particular extension), FHIR will not introduce confusion into
  the implementation community by defining a conflicting mechanism for solving that problem in the core
  specification.

### <span class="sectioncount">?.?.3<a name="?.?.3"> </a></span> Forward compatible behavior

In a typical scenario, mixed versions may need to exist, so applications SHOULD ignore elements 
that they do not recognize unless they are modifierExtensions.
However, in a healthcare context, many application vendors are unwilling to 
consider this approach because of concerns about clinical risk or 
technical limitations in their software (e.g. schema based processing). 
Applications are not required to ignore unknown elements, but SHALL
declare whether they will do so in their [conformance statements](conformance.html).

Unrecognized search criteria SHALL always be ignored.  (Search criteria supported in a query
are echoed as part of the search response so there is no risk in ignoring unexpected search
criteria.)

Attempts to perform HTTP operations on unexpected URLs SHOULD be responded to with an appropriate
error code.    <!-- TODO: Grahame - should this be more explicit? -->

  <!-- Todo - behavior for operations -->

### <span class="sectioncount">?.?.4<a name="?.?.4"> </a></span> Permitted changes for normative content

<table>
  <tbody>
    <tr>
      <th>Category</th><th>Allowed changes</th>
    </tr>
    <tr>
      <td>Elements</td>
      <td>
      Once normative, subsequent versions of 
      this specification may introduce new elements and/or content (e.g. XML attributes, etc.)
      at any point in the bundle, resource and/or data type structures.  However, the names, path 
      and meaning of previously existing data elements will not be changed.
      This includes no change to resource names and no changes to names assigned to slices and
      other elements within profiles.
      </td>
    </tr>
    <tr>
      <td>Cardinality</td>
      <td>
      Minimum element cardinalities will not be changed.  Upper cardinality may change from 1 to * only in circumstances
      where all elements except for the first repetition can be safely ignored.  (This may mean that an order is
      assigned to the repeating items or that there is no preference as to which element is retained.)  Systems should
      follow the rules above for unexpected elements.
      </td>
    </tr>
    <tr>
      <td>Descriptions</td>
      <td>
      Descriptive information about a resource - short labels, definitions, usage notes, aliases, examples, rationale, 
      mappings, etc. may be
      updated or revised to provide additional clarity or guidance, but not in such a manner as to invalidate a
      reasonable interpretation of the previously documented use of an element.  (This does not preclude fixing
      obvious errors.)
      </td>  
    </tr>
    <tr>
      <td>Value Sets</td>
      <td>

        The definition of any value set that is marked as &quot;immutable&quot; will never change.  The expansions for
        immutable value sets may still change if no &quot;stable date&quot; is declared and the value set does not
        restrict code system and/or value set references to specific versions if the referenced code system(s)
        or value set(s) change.

        For non-immutable value sets:

*   Value sets with an enumerated list of codes and having a 'fixed' binding may have additional codes introduced but will never have codes removed.
*   Value sets making use of filters may have filters loosened or tightened to accommodate changes to
          underlying code systems.  StableDates and referenced code system and value set versions may be adjusted
          to point to newer versions.
*   Definitions and display values for codes may change, but only in a manner that would not change          the reasonable interpretation of data captured using the previous definitions or names.
*   Abstract codes may be made concrete.  Concrete codes will not be made abstract.

        For both immutable and non-immutable value sets, additional designations may be declared.

      </td>
    </tr>
    <tr>
      <td>Terminology Bindings</td>
      <td>
      Fixed bindings will remain fixed and will continue to point to the same value set.  If the reference is
      version-specific, it will not change.
      Example bindings and Incomplete bindings may change to point to distinct value sets.  Example bindings
      may be replaced with Incomplete bindings.
      </td>
    </tr>
    <tr>
      <td>Data Types</td>
      <td>
      Data types will not be removed or changed.  New data types may be introduced.  Types declared on existing elements will not be removed or changed.
      Additional data types may be added to elements which are already expressed as a choice of data types only if those elements are optional (minimum cardinality = 0).
      </td>
    </tr>
    <tr>
      <td>Value Constraints</td>
      <td>
      Data types will not be added, removed or changed.  Invariants, regular expressions, fixed values and patterns will not be added, removed or changed.      
      </td>
    </tr>
    <tr>
      <td>Flags</td>
      <td>
        The _Is Modifier_ and _Is Summary_ flags will not be changed.  The _Must Support_ flag may be changed to true, but will not be removed.
      </td>
    </tr>
    <tr>
      <td>Slicing</td>
      <td>
      Slicing rules and aggregation characteristics will not be changed.
      </td>
    </tr>
    <tr>
      <td>Search Criteria</td>
      <td>Search criteria may be added but not removed or renamed.  Existing criteria will not have their type or path changed or
      have their description altered in any way that would invalidate the reasonable behavior of existing systems (with the exception of
      correcting obvious errors).</td>
    </tr>
    <tr>
      <td>Operations</td>    
      <td>
      New operations may be defined but operations may not be removed or renamed.  Existing parameters will not be removed or renamed, nor may their type
      or lower cardinality be changed.  Upper cardinality may be changed from 1 to *.  (Systems should ignore unexpected repetitions.)
      Additional optional parameters may be introduced.
      </td>
    </tr>
    <tr>
      <td>Restful interface</td>
      <td>
      Existing endpoints will not be renamed or removed, nor have their expected behavior changed in a manner that would cause reasonable systems designed
      against prior versions to be non-interoperable.  Additional endpoints may be introduced.
      </td>
    </tr>
    <tr>
      <td>Profiles and extension definitions</td>
      <td>
      Profile structure, extension definitions and search criteria definitions will not be removed or have their 
      URIs changed.  New profile structures, extension definitions and search criteria definitions may be
      introduced.  Profiles may have their statuses changed to &quot;retired&quot;.  Profiles referenced by data elements
      for structures or data types may be replaced
      with a reference to a distinct profile that is &quot;compatible&quot; with the previously referenced profile according
      to these forward and backward compatibility rules.
      </td>
    </tr>
  </tbody>
</table>

Additional discussion on inter-versioning issues can be found here: 
[http://wiki.hl7.org/index.php?title=FHIR_interversion_compatibility](http://wiki.hl7.org/index.php?title=FHIR_interversion_compatibility "FHIR_interversion_compatibility").

</div>