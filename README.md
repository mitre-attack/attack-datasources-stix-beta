# ATT&CK Data Sources STIX Beta

This repository contains mock STIX data demonstrating the new data sources representation coming in ATT&CK v10. 

The included data is formatted as it will appear in future versions of ATT&CK - [documentation of the new data model can be found here](https://github.com/mitre/cti/blob/docs/%23130-data-sources/USAGE.md#data-sources-and-data-components). The data itself however is arbitrary and randomly generated, and does not represent the set of data sources, components, and relationships to techniques which will be published in ATT&CK v10.

The included mock data files are as follows:

| file | description |
|:-----|:------------|
| [enterprise-attack-9.0-only-mock-data-sources.json](/data-sources-only/enterprise-attack-9.0-only-mock-data-sources.json) | STIX 2.0 bundle containing only data sources, data components, relationships, and related techniques -- the portion of the data model depicted in the diagram in the [data model](#data-model) section |
| [enterprise-attack-9.0-only-mock-data-sources-collection.json](/data-sources-only/enterprise-attack-9.0-only-mock-data-sources-collection.json) | STIX 2.1 [collection](https://github.com/center-for-threat-informed-defense/attack-workbench-frontend/blob/develop/docs/collections.md) containing only data sources, data components, relationships, and related techniques  -- the portion of the data model depicted in the diagram in the [data model](#data-model) section |
| [enterprise-attack-9.0-with-mock-data-sources.json](/full-dataset/enterprise-attack-9.0-with-mock-data-sources.json) | STIX 2.0 bundle containing the full Enterprise v9.0 dataset with mock data sources inserted |
| [enterprise-attack-9.0-with-mock-data-sources-collection.json](/full-dataset/enterprise-attack-9.0-with-mock-data-sources-collection.json) | STIX 2.1 [collection](https://github.com/center-for-threat-informed-defense/attack-workbench-frontend/blob/develop/docs/collections.md) containing the full Enterprise v9.0 dataset with mock data sources inserted |

## Data Model

_Note: the contents of this section mirrors [the official data model documentation on MITRE/CTI](https://github.com/mitre/cti/blob/docs/%23130-data-sources/USAGE.md#data-sources-and-data-components). See also [MITRE/CTI#130](https://github.com/mitre/cti/issues/130)._

Data Sources and Data Components represent data which can be used to detect techniques. Data components are nested within a data source but have their own STIX object.

- A Data Component can only have one parent Data Source.
- A Data Source can have any number of Data Components.
- Data Components can map to any number of techniques.

The general structure of data sources and data components is as follows:

<!-- diagram generated with https://asciiflow.com/ -->
```
           "detects"       x_mitre_data_source_ref
          relationship      embedded relationship
               │                      │
┌───────────┐  ▼  ┌────────────────┐  │  ┌───────────┐
│Technique 1│◄────┤                │  │  │           │
└───────────┘     │                │  ▼  │           │
                  │Data Component 1├────►│           │
┌───────────┐     │                │     │           │
│Technique 2│◄────┤                │     │Data Source│
└───────────┘     └────────────────┘     │           │
                                         │           │
┌───────────┐     ┌────────────────┐     │           │
│Technique 3│◄────┤Data Component 2├────►│           │
└───────────┘     └────────────────┘     └───────────┘
```

Prior to ATT&CK v10 data sources were stored in a `x_mitre_data_sources` field on techniques. This representation is still available for backwards-compatibility purposes, and does properly reflect the current set of data sources. However, because information is lost in that representation we advise against using it except in legacy applications. The ATT&CK for ICS domain still uses only the `x_mitre_data_sources` field.

#### Data Sources

A Data Source in ATT&CK is defined by an `x-mitre-data-source` object. As a custom STIX type they follow only the generic [STIX Domain Object pattern](https://docs.oasis-open.org/cti/stix/v2.0/csprd01/part2-stix-objects/stix-v2.0-csprd01-part2-stix-objects.html#_Toc476230920). 

Data Sources extend the generic SDO format with the following fields:

| Field | Type | Description |
|:------|:-----|-------------|
| `x_mitre_platforms` | string[] | List of platforms that apply to the data source. |
| `x_mitre_collection_layers` | string[] | List of places the data can be collected from. |

#### Data Components

A Data Component in ATT&CK is represented as an `x-mitre-data-component` object. As a custom STIX type they follow only the generic [STIX Domain Object pattern](https://docs.oasis-open.org/cti/stix/v2.0/csprd01/part2-stix-objects/stix-v2.0-csprd01-part2-stix-objects.html#_Toc476230920). 

Data Components extend the generic SDO format with the following field:

| Field | Type | Description |
|:------|:-----|-------------|
| `x_mitre_data_source_ref` | embedded relationship (string) | STIX ID of the data source this component is a part of. |
