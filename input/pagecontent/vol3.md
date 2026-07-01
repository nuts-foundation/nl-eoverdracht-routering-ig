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

#### Example FHIR queries

Some example FHIR queries that can be used:

| Description | Query | Common use |
|-------------|-------|------------|
| Look up an Organization by did:nuts-identifier | /Organization?identifier=urn:ietf:rfc:3986\|{did:nuts-identifier including did:nuts-prefix} | Part of nursing handoff flow at Sending Organization, Receiving Organization looks up own Organization-resource |
| Find all Locations of an organization | /Location?organization=Organization/{organization-resource-id} | Part of nursing handoff flow at Sending Organization |
| Find all HealthcareServices of an organization | /HealthcareService?organization=Organization/{organization-resource-id} | Part of nursing handoff flow at Sending Organization |
| Find all HealthcareServices of a specific 'zorgzwaarte' within an organization | /HealthcareService?organization=Organization/{organization-resource-id}&service-type=https://informatiemodel.istandaarden.nl/informatiemodel/iwlz/estafette/2.4/codelijsten/cod163\|{zorgzwaarte-code} | Part of nursing handoff flow at Sending Organization |
| Lookup Location | /Location?identifier={identifier-system found in Task}\|{identifier-value found in Task} | Receiving Organization looks up the targeted Location using the identifier that is mentioned in Task.location |
| Lookup HealthcareService | /HealthcareService?identifier={identifier-system found in Task}\|{identifier-value found in Task} | Receiving Organization looks up the targeted HealthcareService using the identifier that is mentioned in Task.healthcareservice |

### Routing

#### Task

Sending Organizations have to use the following eOverdracht-Task profile:

```json
{
  "resourceType": "StructureDefinition",
  "id": "eOverdracht-Task",
  "url": "http://nictiz.nl/fhir/StructureDefinition/eOverdracht-Task",
  "version": "4.0.0",
  "name": "eOverdrachtTask",
  "title": "eOverdracht Task",
  "status": "active",
  "publisher": "Nictiz",
  "contact": [
    {
      "name": "Nictiz",
      "telecom": [
        {
          "system": "url",
          "value": "https://www.nictiz.nl",
          "use": "work"
        }
      ]
    }
  ],
  "description": "The use cases within eOverdracht form a workflow that may include the negotiation of the transfer of the patient, and ends with the transfer of the medical record. This Task resource is used to track the worflow and acts as the entry point for all data exchanges within eOverdracht.",
  "copyright": "CC0",
  "fhirVersion": "3.0.2",
  "mapping": [
    {
      "identity": "eOverdracht-NursingHandoffAdults",
      "uri": "https://decor.nictiz.nl/art-decor/decor-scenarios--e-overdracht-?id=2.16.840.1.113883.2.4.3.11.60.30.4.39",
      "name": "eOverdracht 4.0 transaction \"Sturen Overdrachtsbericht\""
    },
    {
      "identity": "eOverdracht-NursingHandoffAdults-Answer",
      "uri": "https://decor.nictiz.nl/art-decor/decor-scenarios--e-overdracht-?id=2.16.840.1.113883.2.4.3.11.60.30.4.64",
      "name": "eOverdracht 4.0 transaction \"Sturen antwoord Overdrachtsbericht\""
    }
  ],
  "kind": "resource",
  "abstract": false,
  "type": "Task",
  "baseDefinition": "http://hl7.org/fhir/StructureDefinition/Task",
  "derivation": "constraint",
  "differential": {
    "element": [
  {
        "id": "Task.extension:location",
        "path": "Task.extension",
        "sliceName": "location",
        "min": 0,
        "max": "1",
        "type": [
          {
            "code": "Extension",
            "profile": [
              "http://nuts-foundation.github.io/nl-generic-functions-ig/StructureDefinition/task-stu3-location"
            ]
          }
        ]
      },
      {
        "id": "Task.extension:healthcareservice",
        "path": "Task.extension",
        "sliceName": "healthcareservice",
        "min": 0,
        "max": "1",
        "type": [
          {
            "code": "Extension",
            "profile": [
              "http://nuts-foundation.github.io/nl-generic-functions-ig/StructureDefinition/task-stu3-healthcareservice"
            ]
          }
        ]
      },
      {
        "id": "Task.status",
        "path": "Task.status",
        "definition": "The current state of the Task. States that can be used:\r\n\r\n* _in-progress_: placer has prepared the transfer of the patient\r\n* _completed_: filler received the nursing handoff\r\n\r\nNote: other statuses may be used in the future for the advance notice of the patient transfer.",
        "mapping": [
          {
            "identity": "eOverdracht-NursingHandoffAdults-Answer",
            "map": "e-overdracht-dataelement-v4-1166",
            "comment": "Antwoord aanmelding"
          }
        ]
      },
      {
        "id": "Task.statusReason.text",
        "path": "Task.statusReason.text",
        "mapping": [
          {
            "identity": "eOverdracht-NursingHandoffAdults-Answer",
            "map": "e-overdracht-dataelement-v4-1168",
            "comment": "Toelichting antwoord aanmelding"
          }
        ]
      },
      {
        "id": "Task.intent",
        "path": "Task.intent",
        "comment": "This element is immutable.  Proposed tasks, planned tasks, etc. must be distinct instances.\n\nIn the case the Task has the intent \"order\""
      },
      {
        "id": "Task.code",
        "path": "Task.code",
        "min": 1
      },
      {
        "id": "Task.code.coding",
        "path": "Task.code.coding",
        "slicing": {
          "discriminator": [
            {
              "type": "value",
              "path": "code"
            },
            {
              "type": "value",
              "path": "system"
            }
          ],
          "rules": "open"
        },
        "min": 1
      },
      {
        "id": "Task.code.coding:taskCode",
        "path": "Task.code.coding",
        "sliceName": "taskCode",
        "min": 1,
        "max": "1"
      },
      {
        "id": "Task.code.coding:taskCode.system",
        "path": "Task.code.coding.system",
        "min": 1,
        "fixedUri": "http://snomed.info/sct"
      },
      {
        "id": "Task.code.coding:taskCode.code",
        "path": "Task.code.coding.code",
        "min": 1,
        "fixedCode": "308292007"
      },
      {
        "id": "Task.for",
        "path": "Task.for",
        "min": 1,
        "type": [
          {
            "code": "Reference",
            "targetProfile": "http://fhir.nl/fhir/StructureDefinition/nl-core-patient"
          }
        ],
        "mapping": [
          {
            "identity": "eOverdracht-NursingHandoffAdults",
            "map": "e-overdracht-dataelement-v4-4",
            "comment": "Persoonsgegevens::Patient"
          }
        ]
      },
      {
        "id": "Task.requester",
        "path": "Task.requester",
        "min": 1
      },
      {
        "id": "Task.requester.agent",
        "path": "Task.requester.agent",
        "definition": "The practitioner or organisation who initiated the task.",
        "comment": "This element is usually populated with the sending organization (Sturende organisatie::Zorgaanbieder in the eOverdracht dataset). However, if there is a need by the sending organization to communicate the health professional who initiated the transfer request, this element can be populated with this person and the sending organization is communicated using `.onBehalfOf`.\r\n\r\nA health professional communicated here pertains the practical act of initiating the transfer request. The health profession who is responsible for the content is communicated using `Composition.author`. These two persons can be the same person.",
        "type": [
          {
            "code": "Reference",
            "targetProfile": "http://fhir.nl/fhir/StructureDefinition/nl-core-organization"
          },
          {
            "code": "Reference",
            "targetProfile": "http://fhir.nl/fhir/StructureDefinition/nl-core-practitioner"
          }
        ],
        "mapping": [
          {
            "identity": "eOverdracht-NursingHandoffAdults",
            "map": "e-overdracht-dataelement-v4-102",
            "comment": "Sturende organisatie::Zorgaanbieder"
          }
        ]
      },
      {
        "id": "Task.requester.agent.extension:practitionerRole",
        "path": "Task.requester.agent.extension",
        "sliceName": "practitionerRole",
        "max": "1",
        "type": [
          {
            "code": "Extension",
            "profile": "http://nictiz.nl/fhir/StructureDefinition/practitionerrole-reference"
          }
        ]
      },
      {
        "id": "Task.requester.agent.extension:practitionerRole.url",
        "path": "Task.requester.agent.extension.url",
        "fixedUri": "http://nictiz.nl/fhir/StructureDefinition/practitionerrole-reference"
      },
      {
        "id": "Task.requester.onBehalfOf",
        "path": "Task.requester.onBehalfOf",
        "comment": "This element is populated with the sending organization (Sturende organisatie::Zorgaanbieder in the eOverdracht dataset) only when `.agent` contains a reference to a health professional. If this is not the case, the sending organization is communicated using `.agent`.",
        "type": [
          {
            "code": "Reference",
            "targetProfile": "http://hl7.org/fhir/StructureDefinition/Organization"
          },
          {
            "code": "Reference",
            "targetProfile": "http://fhir.nl/fhir/StructureDefinition/nl-core-practitioner"
          }
        ],
        "mapping": [
          {
            "identity": "eOverdracht-NursingHandoffAdults",
            "map": "e-overdracht-dataelement-v4-102",
            "comment": "Sturende organisatie::Zorgaanbieder"
          }
        ]
      },
      {
        "id": "Task.owner",
        "path": "Task.owner",
        "type": [
          {
            "code": "Reference",
            "targetProfile": "http://fhir.nl/fhir/StructureDefinition/nl-core-organization"
          }
        ],
        "mapping": [
          {
            "identity": "eOverdracht-NursingHandoffAdults",
            "map": "e-overdracht-dataelement-v4-153",
            "comment": "Ontvangende organisatie::Zorgaanbieder"
          },
          {
            "identity": "eOverdracht-NursingHandoffAdults-Answer",
            "map": "e-overdracht-dataelement-v4-153",
            "comment": "Ontvangende organisatie::Zorgaanbieder"
          }
        ]
      },
      {
        "id": "Task.input",
        "path": "Task.input",
        "slicing": {
          "discriminator": [
            {
              "type": "value",
              "path": "type.coding.code"
            }
          ],
          "rules": "open"
        }
      },
      {
        "id": "Task.input:nursingHandoff",
        "path": "Task.input",
        "sliceName": "nursingHandoff",
        "max": "1"
      },
      {
        "id": "Task.input:nursingHandoff.type.coding",
        "path": "Task.input.type.coding",
        "slicing": {
          "discriminator": [
            {
              "type": "value",
              "path": "system"
            },
            {
              "type": "value",
              "path": "code"
            }
          ],
          "rules": "open"
        },
        "min": 1
      },
      {
        "id": "Task.input:nursingHandoff.type.coding:nursingHandoffCode",
        "path": "Task.input.type.coding",
        "sliceName": "nursingHandoffCode",
        "min": 1,
        "max": "1"
      },
      {
        "id": "Task.input:nursingHandoff.type.coding:nursingHandoffCode.system",
        "path": "Task.input.type.coding.system",
        "min": 1,
        "fixedUri": "http://snomed.info/sct"
      },
      {
        "id": "Task.input:nursingHandoff.type.coding:nursingHandoffCode.code",
        "path": "Task.input.type.coding.code",
        "min": 1,
        "fixedCode": "11171000146100"
      },
      {
        "id": "Task.input:nursingHandoff.value[x]:valueReference",
        "path": "Task.input.value[x]",
        "sliceName": "valueReference",
        "type": [
          {
            "code": "Reference",
            "targetProfile": "http://nictiz.nl/fhir/StructureDefinition/eOverdracht-NursingHandoff-Childcare-0-1yo"
          },
          {
            "code": "Reference",
            "targetProfile": "http://nictiz.nl/fhir/StructureDefinition/eOverdracht-NursingHandoff-Childcare-1-18yo"
          },
          {
            "code": "Reference",
            "targetProfile": "http://nictiz.nl/fhir/StructureDefinition/eOverdracht-NursingHandoff-Adults"
          }
        ]
      }
    ]
  }
}
```

Example:

```json
{
  "extension": [
    {
      "url": "http://nuts-foundation.github.io/nl-generic-functions-ig/StructureDefinition/task-stu3-healthcareservice",
      "valueReference": {
        "reference": "HealthcareService/b48826dc-2d58-479a-bfd3-80b7a9d69757",
        "display": "Organization 3 - HealthcareService Verpleging"
      }
    },
    {
      "url": "http://nuts-foundation.github.io/nl-generic-functions-ig/StructureDefinition/task-stu3-location",
      "valueReference": {
        "reference": "Location/9a2b8f1c-4e7d-42a1-b3c9-2d5e8f7a6c1b",
        "display": "Organization 3 - Location Nursing Department"
      }
    }
  ],
  "resourceType": "Task",
  "intent": "order",
  "for": {
    "reference": "Patient/nl-core-patient-eov-test-1-1b-01",
    "display": "Erik XXX_Altenborg"
  },
  "input": [
    {
      "valueReference": {
        "reference": "Composition/eOverdracht-AdvanceNotice-eov-test-1-1b-01",
        "display": "Aanmeldbericht Erik XXX_Altenborg"
      },
      "type": {
        "coding": [
          {
            "display": "Admission request document",
            "code": "721915006",
            "system": "http://snomed.info/sct"
          }
        ]
      }
    }
  ],
  "id": "eOverdracht-Task-eov-test-1-1b",
  "requester": {
    "agent": {
      "extension": [
        {
          "url": "http://nictiz.nl/fhir/StructureDefinition/practitionerrole-reference",
          "valueReference": {
            "reference": "PractitionerRole/nl-core-practitionerrole-eov-test-1-1b-01",
            "display": "Verpleegkundige, niet nader gespecificeerd"
          }
        }
      ],
      "reference": "Practitioner/nl-core-practitioner-eov-test-1-1b-01",
      "display": "C.M. Bruinsma"
    },
    "onBehalfOf": {
      "reference": "Organization/nl-core-organization-eov-test-1-1b-01",
      "display": "AB-zkh Noord"
    }
  },
  "code": {
    "coding": [
      {
        "display": "Overdracht van zorg",
        "code": "308292007",
        "system": "http://snomed.info/sct"
      }
    ]
  },
  "status": "requested",
  "owner": {
    "reference": "Organization/nl-core-organization-eov-test-1-1b-02",
    "display": "Thuiszorg Org Noord"
  },
  "meta": {
    "profile": [
      "https://nuts-foundation.github.io/nl-generic-functions-ig/eOverdracht-Task-STU3-profile.json"
    ]
  }
}
```



