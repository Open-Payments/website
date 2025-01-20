---
description: Workflow Definition - Format Specification
---

# Workflow Definition

### Overview <a href="#overview" id="overview"></a>

The Workflow Definition format specifies the structure and sequence of tasks required to process a message in the Open Payments system. Each workflow is event-driven, with tasks executing based on the message's processing state and previous task results.

### Specification <a href="#specification" id="specification"></a>

#### Workflow Structure

```json
{
  "id": "string",                    // Unique identifier for the workflow
  "name": "string",                  // Descriptive name
  "description": "string",           // Detailed description of workflow's purpose
  "version": "integer",              // Version number of the workflow definition
  "tenant": "string",                // Tenant identifier
  "origin": "string",                // Origin of the workflow (e.g., "api")
  "status": "string",                // Status: Active, Draft, or Deprecated
  "condition": "object|null",        // Optional workflow-level condition
  "input_topic": "string",           // Input message topic
  "tasks": [                         // Array of tasks in the workflow
    {
      "id": "string",                // Unique identifier for the task
      "name": "string",              // Descriptive name of the task
      "description": "string",       // Description of what the task does
      "message_status": "string",    // Current message processing status
      "prev_task": "string",         // Previous task identifier
      "prev_status_code": "string",  // Required status from previous task
      "condition": "object|null",    // Optional task-specific condition
      "function": "string",          // Function type: Parse, Fetch, or Enrich
      "input": "object"              // Function-specific configuration
    }
  ],
  "persist_on_complete": "boolean"   // Whether to persist completed messages
}
```

### Functions

#### 1. Parse

Parses incoming messages in specific formats (e.g., ISO20022).

```json
{
  "function": "Parse",
  "input": {}  // Configuration depends on message format
}
```

#### 2. Fetch

Retrieves data from external systems or services.

```json
{
  "function": "Fetch",
  "input": {
    "data_type": {                // Type of data to fetch
      "field1": "value1",         // Data-specific configuration
      "field2": "value2"
    }
  }
}
```

#### 3. Enrich

Enriches message with additional data or modifications.

```json
{
  "function": "Enrich",
  "input": [
    {
      "field": "string",          // Target field path
      "logic": "object",          // Logic for dynamic values
      "value": "any",             // Static value to set
      "description": "string"     // Description of the enrichment
    }
  ]
}
```

### Error Handling

Tasks can define error handling paths by specifying tasks that trigger on failure status codes:

```json
{
  "id": "error_handler",
  "name": "Handle Error Condition",
  "prev_task": "main_task",
  "prev_status_code": "Failure",
  "function": "Enrich",
  "input": [
    {
      "field": "metadata.error_code",
      "value": "ERROR_CODE",
      "description": "Set error code"
    },
    {
      "field": "metadata.error_description",
      "value": "Error description",
      "description": "Set error description"
    }
  ]
}
```

### Message Status States

* `Received`: Initial state for new messages
* `Processing`: Message is being processed
* `Failed`: Processing failed
* `Completed`: Processing completed successfully

### Key Concepts

#### **Event-Driven Execution**

* Tasks execute based on message status and previous task results
* Each task specifies required previous task and status
* Processing continues until completion or terminal error state

#### **Task Functions**

* Parse: Handles initial message parsing
* Fetch: Retrieves external data
* Enrich: Modifies message content

#### **Message Processing**

* Message state tracked via status field
* Previous task results determine next execution
* Error handling paths for failure scenarios

## Best Practices

#### **Task Naming**

* Use clear, descriptive task IDs
* Follow consistent naming convention
* Include purpose in description

#### **Error Handling**

* Define specific error handlers for critical tasks
* Set appropriate error codes and descriptions
* Consider all potential failure scenarios

#### **Function Configuration**

* Use meaningful field paths
* Document data transformations
* Handle missing or invalid data

#### **Workflow Organization**

* Group related tasks logically
* Maintain clear task progression
* Include error handling paths
* Consider monitoring and maintenance needs
