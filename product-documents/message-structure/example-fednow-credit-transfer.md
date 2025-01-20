# Example: FedNow Credit Transfer

```json
{
  "id": 20241029123456,
  "parent_id": null,
  "payload": {
    "storage": "Inline",
    "content": {
      "creditTransferMessage": {
        "messageId": "BFFF/120928-FEDNOW/123456",
        "creditorAccount": "9876543210",
        "amount": "1000.00",
        "debtorAccount": "1234567890"
      }
    },
    "schema": "ISO20022",
    "format": "JSON",
    "encoding": "UTF-8",
    "size": 428
  },
  "version": 1,
  "tenant": "BANK_USA_001",
  "origin": "CORE_BANKING",
  "processing": {
    "status": "processing",
    "workflow_id": "FEDNOW_CREDIT_TRANSFER_V1",
    "prev_task": "validation",
    "prev_status_code": "SUCCESS",
    "timestamp": "2024-10-29T14:30:01.523Z"
  },
  "data": {
    "messageType": "pacs.008.001.09",
    "businessMessageIdentifier": "BFFF/120928-FEDNOW/123456",
    "creditTransferTransaction": {
      "paymentIdentification": {
        "instructionIdentification": "INSTR-ID-123456",
        "endToEndIdentification": "E2E-REF-123456",
        "transactionIdentification": "TXID-123456"
      },
      "paymentTypeInformation": {
        "localInstrument": "STANDARD",
        "categoryPurpose": {
          "code": "CASH"
        }
      },
      "interbankSettlementAmount": {
        "amount": "1000.00",
        "currency": "USD"
      },
      "chargeBearer": "SLEV",
      "debtor": {
        "name": "John Smith",
        "identification": {
          "privateIdentification": {
            "other": {
              "identification": "DEB-123456"
            }
          }
        },
        "contactDetails": {
          "emailAddress": "john.smith@email.com"
        }
      },
      "debtorAccount": {
        "identification": {
          "accountNumber": "1234567890"
        },
        "type": "CACC"
      },
      "debtorAgent": {
        "financialInstitutionIdentification": {
          "clearingSystemIdentification": {
            "code": "USABA"
          },
          "clearingSystemMemberIdentification": "021000021"
        }
      },
      "creditor": {
        "name": "Jane Doe",
        "identification": {
          "privateIdentification": {
            "other": {
              "identification": "CRED-789012"
            }
          }
        }
      },
      "creditorAccount": {
        "identification": {
          "accountNumber": "9876543210"
        },
        "type": "CACC"
      },
      "creditorAgent": {
        "financialInstitutionIdentification": {
          "clearingSystemIdentification": {
            "code": "USABA"
          },
          "clearingSystemMemberIdentification": "021000022"
        }
      },
      "purpose": {
        "code": "CASH"
      },
      "remittanceInformation": {
        "unstructured": "Invoice payment #INV-2024-001"
      },
      "settlementInformation": {
        "settlementMethod": "CLRG",
        "clearingSystem": "FEDNOW"
      }
    }
  },
  "metadata": {
    "format_version": "ISO20022:2019",
    "type": "credit_transfer",
    "priority": "real-time",
    "tags": ["fednow", "domestic", "credit_transfer"],
    "flags": {
      "requires_compliance_check": true,
      "is_cross_border": false,
      "requires_funds_check": true
    },
    "customer_risk_score": 3,
    "customer_category": "MEDIUM",
    "exchange_rate": 0.92
  },
  "audit": [
    {
      "id": 1,
      "start_time": "2024-10-29T14:30:00.100Z",
      "finish_time": "2024-10-29T14:30:00.120Z",
      "workflow": "FEDNOW_CREDIT_TRANSFER_V1",
      "workflow_version": 1,
      "task": "reception",
      "description": "Message received and initial parsing completed",
      "changes": [
        {
          "field": "processing.status",
          "type": "create",
          "timestamp": "2024-10-29T14:30:00.100Z",
          "old_value": null,
          "new_value": "received",
          "reason": "Initial message reception",
          "rule_id": "INIT_001"
        }
      ]
    },
    {
      "id": 2,
      "start_time": "2024-10-29T14:30:00.500Z",
      "finish_time": "2024-10-29T14:30:00.530Z",
      "workflow": "FEDNOW_CREDIT_TRANSFER_V1",
      "workflow_version": 1,
      "task": "enrichment",
      "description": "Enriched payment with customer and compliance information",
      "changes": [
        {
          "field": "data.creditTransferTransaction.debtor.contactDetails",
          "type": "create",
          "timestamp": "2024-10-29T14:30:00.500Z",
          "old_value": null,
          "new_value": {
            "emailAddress": "john.smith@email.com"
          },
          "reason": "Added customer contact details",
          "rule_id": "ENRICH_001"
        }
      ]
    },
    {
      "id": 3,
      "start_time": "2024-10-29T14:30:01.500Z",
      "finish_time": "2024-10-29T14:30:01.523Z",
      "workflow": "FEDNOW_CREDIT_TRANSFER_V1",
      "workflow_version": 1,
      "task": "validation",
      "description": "Validated message against FedNow requirements",
      "changes": [
        {
          "field": "processing.status",
          "type": "update",
          "timestamp": "2024-10-29T14:30:01.523Z",
          "old_value": "received",
          "new_value": "processing",
          "reason": "Validation successful, proceeding with processing",
          "rule_id": "VAL_001"
        }
      ]
    }
  ]
}
```
