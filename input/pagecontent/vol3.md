Volume 3 of this specification describes the agreements and specifications about content.

### Generic Function Addressing

Receiving Organizations and their locations, departments, teams, healthcare services and specialties have to be registered at the LRZa using the generic function Addressing. This page contains agreements and specifications that are specific to eOverdracht.

#### Organization

Receiving organizations have to be modelled as [Organization](https://minvws.github.io/generiekefuncties-docs/en/care-services.html#organization) resources using the generic function Addressing specification. 
The Organization-resource of the Receiver Organization MUST include an identifier element that contains its did:nuts-identifier:
- `identifier.system` : `"urn:ietf:rfc:3986"`
- `identifier.value` : The full did:nuts-string of the Receiver Organization (e.g., "did:nuts:123456789abcdefghi")

#### Location

Locations and departments of receiving organizations have to be modeled as [Location](https://minvws.github.io/generiekefuncties-docs/en/care-services.html#location) resources using the generic function Addressing specification. 

#### Healthcare services

Teams, healthcare services and specialties have to be modeled as [HealthcareService](https://minvws.github.io/generiekefuncties-docs/en/care-services.html#healthcareservice) resources using the generic function Addressing specification. 

#### Other resources

Regarding the generic function Addressing no other resources than Organization, Location and HealthcareService are in scope.
