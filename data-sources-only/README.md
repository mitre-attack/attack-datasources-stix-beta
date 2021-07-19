# Data Sources Only Mock Data

The data in this folder includes only the portion of the full ATT&CK data model relevant to the data sources themselves -- the portion reflected in the following diagram:

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

| file | description |
|:-----|:------------|
| [enterprise-attack-9.0-only-mock-data-sources.json](/data-sources-only/enterprise-attack-9.0-only-mock-data-sources.json) | STIX 2.0 bundle containing only data sources, data components, relationships, and related techniques |
| [enterprise-attack-9.0-only-mock-data-sources-collection.json](/data-sources-only/enterprise-attack-9.0-only-mock-data-sources-collection.json) | STIX 2.1 [collection](https://github.com/center-for-threat-informed-defense/attack-workbench-frontend/blob/develop/docs/collections.md) containing only data sources, data components, relationships, and related techniques |

