# Message Structure

## Overview <a href="#overview" id="overview"></a>

The Message Structure defines the JSON format used by the Open Payments system to handle incoming messages. This structure is designed to be **generic** and **adaptable**, capable of supporting various message standards across different domains.

### Key characteristics:

* Generic structure for multiple use cases
* Domain-specific content encapsulation
* Clear separation of concerns
* Support for multi-tenant deployments

## Architecture <a href="#architecture" id="architecture"></a>

The structure is organized into distinct sections:

### Root-Level Fields <a href="#root-level-fields" id="root-level-fields"></a>

Essential fields that the message processor uses for core operations:

* `id`: Unique message identifier
* `payload`: Original message content
* `tenant`: Multi-tenant identifier
* `origin`: Source information
* `processing`: Processing state
* `auditlog`: Processing history

### Domain-Specific Sections <a href="#domain-specific-sections" id="domain-specific-sections"></a>

* `data`: Contains the standardized message content (e.g., ISO20022 for payments)
* `metadata`: Additional context and processing instructions

## Standards Support

### Payments Domain <a href="#payments-domain" id="payments-domain"></a>

When used for payment processing:

* `data` section contains ISO20022-compliant message structures
* Standard formats like pacs.008 for credit transfers are supported
* Maintains compliance with payment scheme requirements

### Other Domains <a href="#other-domains" id="other-domains"></a>

The structure can accommodate various standards:

* Different message formats can be incorporated
* Domain-specific validations can be implemented
* Custom workflows can be defined
