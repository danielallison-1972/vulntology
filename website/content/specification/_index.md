---
title: "Specification"
menu:
  primary:
    name: Specification
    weight: 50
sidenav:
  activerenderdepth: 2
---

# The NIST Vulntology Specification

The following and related sections describe the Vulntology specification.

## Conventions Used in this Document

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [BCP 14](https://www.rfc-editor.org/info/bcp14) [RFC2119](https://www.rfc-editor.org/rfc/rfc2119.html) [RFC8174](https://www.rfc-editor.org/rfc/rfc8174.html) when, and only when, they appear in all capitals, as shown here.

## The Components

The Vulntology framework is composed of simple components described below:

- **Objects**: A Conceptual entity; Objects can be related to other objects, have types, relationships, and properties. Each object, such as [Vulnerability](objects/vulnerability), can have multiple properties and/or relationships with other components. 

  - **Relationships**: A connection relating one object to another. Relationships retain an expected cardinality, i.e. or `one to many` or `zero to many`.

  - **Properties**: A connection between an object and a value. Some properties and associated values relate to or drive the use of other properties.

  The top level object to begin with when reviewing the components is the [Vulnerability](objects/vulnerability) object.

- **Values**: An explicit characteristic used to describe a detail of a Type or SubType. A list of value sets defined by the Vulntology framework is located under the [values](values) directory. Values are contained within Type and SubType groups such as [Theatre](values/theater).

  - **Type/SubType**: Types and subtypes are categorizations and/or groupings of values. Subtypes are applicable to a specific value within a parent Type.

## Visuals and Examples

### Visuals

![Vulntology Graph](/figures/vulntology-graph.png "Vultology Graph")

The graph above illustrates how all of the components defined in the Vulntology relate to each other.

To see at a very high level how the Vulntology framework builds on the current methodology of describing vulnerabilities. Refer to the [High Level Model](/about/#high-level-view).

### Examples

To assist with understanding how all of the components would work together in a real world application, we have provided a generic Cross Site Scripting vulnerability in both human readable text and graph form. The human readable text is derived from the graph format data. This displays how human readable descriptions can be derived from a Vulntology representation of a vulnerability. <br />

#### Human Readable Text
---
Legend:<br />
**Object**&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;[**Object Instantiation**]&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;*Property*&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;[*Value*]<br />

There is a **vulnerability**, *known as* [*CVE-2050-1234*].<br />
It is of importance to the [*Industrial Control System*] and [*Health Care*] *sectors*.<br />
The **vulnerability** is due to code that originates from [*Fake FakeProduct 1.0.0.*] <br />
The **vulnerability** [*CVE-2050-1234*] has one **scenario** that is an [*internet*] based [*cross-site scripting*]. <br />
The [**first**] **scenario** is *evidenced by* [*www.acme.com*]<br />
The [**first**] **scenario** *affects product* [*Fake FakeProduct 1.0.0.*] <br />
The [**first**] **scenario** is *blocked by* **social engineering** of an [*application*] [*user*] via a [*malicious link*] and requiring [*user*] [*application*] privileges. <br />
The [**first**] **action** of the [**first**] **scenario** is [*code execution*] to the [*webserver*] which is the [*primary security authority*].<br />
The [**first**] **impact** of the [**first**] **action** is a [*low*] *criticality*, [*limited*] *scope*, [*direct write*].<br />
The [**second**] **action** of the [**first**] **scenario** is [*code execution*] to the [*browser*] which is the [*secondary security authority*].<br />
The [**first**] **impact** of the [**second**] **action** is a [*low*] *criticality*, [*limited*] *scope*, [*direct write*].<br />
The [**second**] **impact** of the [**second**] **action** is a [*low*] *criticality*, [*limited*] *scope*, [*direct read*]. <br />

#### Graph
---
![XSS Example](/figures/xss-example.png "XSS Example")

#### JSON
---
```json
{
  "Vulnerability": {
    "hasIdentity": [
      {
        "scheme": "http://cve.mitre.org",
        "value": "CVE-2050-1234"
      }
    ],
    "hasOriginatingProduct": {
      "hasProductEnumeration": [
        {
          "scheme": "https://csrc.nist.gov/pubs/ir/7695/final",
          "values": [
            "cpe:2.3:a:fake:fakeproductX:1.0.0:*:*:*:*:*:*:*"
          ]
        }
      ],
      "hasCPEApplicabilityStatement": []
    },
    "hasScenario": [
      {
        "id": "b4c3887f-28dd-4226-9872-6f44803f1c4b",
        "requiresAttackTheatre": "Remote::Internet",
        "hasExploitedWeakness": [
          "CWE-79"
        ],
        "evidencedBySource": [
          {
            "url": "https://www.acme.com",
            "tag": "vendor-advisory"
          }
        ],
        "affectsProduct": {
          "hasProductEnumeration": [
            {
              "scheme": "https://csrc.nist.gov/pubs/ir/7695/final",
              "values": [
                "cpe:2.3:a:fake:fakeproductX:1.0.0:*:*:*:*:*:*:*"
              ]
            }
          ],
          "hasCPEApplicabilityStatement": []
        },
        "hasAction": [
          {
            "id": "bd095f8b-b83b-49dc-a2f0-79fd47927147",
            "hasImpactMethod": [
              {
                "hasImpactMethodType": "Code Execution"
              }
            ],
            "affectsContext": "Application::Web Server",
            "hasEntityRole": "Security Authority::Primary",
            "resultsInImpact": [
              {
                "id": "ceb33a58-68cc-4edd-9a5d-0f3c3009ed32",
                "hasCriticality": "Low",
                "hasScope": "Limited",
                "hasPhysicalImpact": "Physical Resource Consumption"
              },
              {
                "id": "17238185-e8ca-4ec7-9db3-bea8b9a2dcde",
                "hasCriticality": "Low",
                "hasScope": "Limited",
                "hasLogicalImpact": "Write Direct",
                "hasLocation": "File System"
              }
            ],
            "doesNotResultInImpact": [
              {
                "id": "25395ff2-19a0-4545-a940-44d0b2a2e0b1",
                "hasCriticality": "Low",
                "hasScope": "Limited",
                "hasLogicalImpact": "Service Interrupt::Hang",
                "hasLocation": "Network Traffic"
              },
              {
                "id": "220d45a1-0086-41c2-b08e-62080a39127d",
                "hasCriticality": "Low",
                "hasScope": "Limited",
                "hasPhysicalImpact": "Human Injury"
              }
            ],
            "name": "vulnEx1_S1_A1"
          },
          {
            "id": "05583e58-eb45-494a-867f-4230e0fa464a",
            "hasImpactMethod": [
              {
                "hasImpactMethodType": "Code Execution"
              }
            ],
            "affectsContext": "Application",
            "hasEntityRole": "Security Authority::Secondary",
            "resultsInImpact": [
              {
                "id": "702f3005-5de6-468f-afd1-c3e338cee6fc",
                "hasCriticality": "Low",
                "hasScope": "Limited",
                "hasLogicalImpact": "Read Direct",
                "hasLocation": "Memory"
              },
              {
                "id": "dc1d7268-2425-4a36-8a81-f80dbbc4d66d",
                "hasCriticality": "Low",
                "hasScope": "Limited",
                "hasPhysicalImpact": "Physical Resource Consumption"
              }
            ],
            "doesNotResultInImpact": [
              {
                "id": "8443ffa0-f0ed-4866-a91d-5d84160973e2",
                "hasCriticality": "Low",
                "hasScope": "Limited",
                "hasLogicalImpact": "Service Interrupt::Hang",
                "hasLocation": "Network Traffic"
              },
              {
                "id": "1456f0a2-46d9-46ca-9189-4f55816e553e",
                "hasCriticality": "Low",
                "hasScope": "Limited",
                "hasPhysicalImpact": "Human Injury"
              }
            ],
            "name": "vulnEx1_S1_A2"
          }
        ],
        "blockedByBarrier": [
          {
            "id": "11741bd2-c5ee-47e8-bd46-ffaf908a5f1c",
            "hasBarrierType": "Authentication/Authorization::Impersonation::Social Engineering",
            "hasEngineeringMethod": [
              "Malicious Link"
            ],
            "hasNeededPrivilege": "User",
            "relatesToContext": "Application"
          }
        ],
        "name": "vulnEx1_S1"
      }
    ],
    "hasSectorOfInterest": [
      "Industrial Control System",
      "Health Care"
    ]
  }
}
```
