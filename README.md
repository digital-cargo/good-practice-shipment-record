<!--
---
title: shipment-tracking
repository: https://github.com/digital-cargo/good-practice-shipment-tracking
version: 1.0.0
maintainers: 
- Daniel A. Doeppner
- Ingo Zeschky
- Philipp Billion
ontologies:
- https://onerecord.iata.org/ns/cargo/3.0.0
- https://onerecord.iata.org/ns/api/2.0.0
- https://onerecord.iata.org/ns/coreCodeLists/0.0.3
data-classes:
- tbd
data-properties:
- tbd
api-version:
- 2.0.0
api-endpoints:
- method: GET 
  path: /logistics-objects/{logisticsObjectId} 
- method: GET 
  path: /logistics-objects/{logisticsObjectId}
- method: GET 
  path: /logistics-objects/{logisticsObjectId}/logistics-events
- method: GET 
  path: /logistics-objects/{logisticsObjectId}/logistics-events/{logisticsEventId}
- method: POST 
  path: /notifications
- method: GET 
  path: /subscriptions
- method: POST 
  path: /subscriptions
- method: GET 
  path: /action-requests/{actionRequestId} 
- method: DELETE
  path: /action-requests/{actionRequestId}
---
-->

# Good Practice: ShipmentTracking
[![Made with love for Digital Cargo](https://img.shields.io/badge/Made%20with%20%E2%9D%A4%20for-Digital%20Cargo-dce435)](https://digital-cargo.org)
[![GitHub](https://img.shields.io/github/license/digital-cargo/good-practice-shipment-tracking)](https://creativecommons.org/licenses/by/4.0/)
[![Releases](https://img.shields.io/github/v/release/digital-cargo/good-practice-shipment-tracking)](https://github.com/digital-cargo/good-practice-shipment-tracking/releases)

## Abstract

This is a placeholder for a Good Practice for how to implement the Air Cargo Shipment Record in the IATA ONE Record Data Sharing Standard.

## Introduction

tbd

## Scope


## Glossary
see [digita-cargo/glossary](https://github.com/digital-cargo/glossary)

## References

- ...
- ...
- ...
  
## Acknowledgements

## Community

### Contribute

See [CONTRIBUTING](CONTRIBUTING.md) for more details on how to contribute on this good practice.

### Issues
Issues related to this good practice are tracked on GitHub

- [View open issues](https://github.com/digital-cargo/good-practice-shipment-tracking/issues)
- [Create a new issue](https://github.com/digital-cargo/good-practice-shipment-tracking/issues/new)

### Maintainers

> Each good practice MUST have at least one maintainer who is responsible for ongoing development and quality assurance. 
> Every maintainer MUST have commit access to the good practice repository.

_(sorted alphabetically)_

### Contributors

> Every good practice is the result of the work of the community, and therefore the contribution of each individual should be recognized and appreciated. 
> Below is a list of all the people who have actively contributed to this good practice.

_(sorted alphabetically)_


