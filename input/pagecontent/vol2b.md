### Bolt eOverdracht

The following additions to the sequence diagram in [section 5.3 of the Bolt eOverdracht](https://nuts-foundation.gitbook.io/bolts/eoverdracht/leveranciersspecificatie#id-5.3-ophalen-overdrachtsbericht) are needed:
- Generic Function Addressing
    - Receiving Organization registers Organizations, Locations and HealthcareServices at LRZa
    - Sending Organization and Receiving Organization synchronize data from LRZa to local replica directory
    - Sending Organization queries Organizations, Locations and HealthcareServices at local replica directory
    - Receiving Organization looks up Locations and HealthcareServices at local replica directory

### Receiving Organization registers Organizations, Locations and HealthcareServices at LRZa

See the following sequence diagram of the generic function Addressing specification:
- [Admin Registers Affiliation, Service Provider Publishes Resources](https://minvws.github.io/generiekefuncties-docs/en/care-services.html#use-case-1-admin-registers-affiliation-service-provider-publishes-resources)

### Sending Organization and Receiving Organization synchronize data from LRZa to local replica directory

See the following sequence diagrams of the generic function Addressing specification: 
- [Update Client Initial Load](https://minvws.github.io/generiekefuncties-docs/en/care-services.html#use-case-2a-update-client-initial-load)
- [Update Client Incremental Sync](https://minvws.github.io/generiekefuncties-docs/en/care-services.html#use-case-2b-update-client-incremental-sync)
- [Optimistic Locking on Update](https://minvws.github.io/generiekefuncties-docs/en/care-services.html#use-case-3-healthcare-service-query)

### Sending Organization queries Organizations, Locations and HealthcareServices at local replica directory

See the following sequence diagram of the generic function Addressing specification: 
- [Healthcare service Query](https://minvws.github.io/generiekefuncties-docs/en/care-services.html#use-case-3-healthcare-service-query)

Commons FHIR queries to be used are specified in Volume 3.

### Receiving Organization looks up Locations and HealthcareServices at local replica directory

See the following sequence diagram of the generic function Addressing specification: 
- [Healthcare service Query](https://minvws.github.io/generiekefuncties-docs/en/care-services.html#use-case-3-healthcare-service-query)

Commons FHIR queries to be used are specified in Volume 3.
