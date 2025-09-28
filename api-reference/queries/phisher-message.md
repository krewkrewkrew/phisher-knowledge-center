# PhishER GraphQL Query: phisherMessage

## Overview

Returns a PhishER message by ID. This query allows you to retrieve detailed information about a specific message that has been reported to PhishER.

## Query Signature

```graphql
query phisherMessage($id: String!): PhisherMessage
```

## Arguments

| Attribute | Type | Description | Required |
|-----------|------|-------------|----------|
| `id` | String! | Unique identifier for the message | Yes |

## Return Type: PhisherMessage

The query returns a `PhisherMessage` object with the following fields:

### Core Message Fields

| Field | Type | Description | Null |
|-------|------|-------------|------|
| `id` | String | Unique identifier for the message | No |
| `subject` | String | Subject of the message | Yes |
| `from` | String | Sender's email address | Yes |
| `reportedBy` | String | The person who reported the message | Yes |

### Status and Classification

| Field | Type | Description | Null |
|-------|------|-------------|------|
| `actionStatus` | ActionStatuses | Action status of the message | Yes |
| `pipelineStatus` | String | Pipeline processing status | Yes |
| `category` | Categories | The message's category (CLEAN, SPAM, THREAT, etc.) | Yes |
| `severity` | String | The message's severity level | Yes |

### Message Content and Analysis

| Field | Type | Description | Arguments | Null |
|-------|------|-------------|-----------|------|
| `attachments` | [PhisherPart] | Collection of attachments | `status: ScanStatuses` | Yes |
| `links` | [PhisherLink] | Collection of links found in message | `status: ScanStatuses` | Yes |
| `headers` | [PhisherHeader] | Collection of email headers | - | Yes |
| `rawUrl` | String | URL to download the raw message | - | Yes |
| `phishmlReport` | String | PhishML analysis report | - | Yes |

### Workflow and Management

| Field | Type | Description | Null |
|-------|------|-------------|------|
| `comments` | [PhisherComment] | Collection of comments on the message | Yes |
| `events` | [PhisherMessageEvent] | Collection of events associated with message | Yes |
| `rules` | [PhisherRule] | Set of rules applied to the message | Yes |
| `tags` | [PhisherTag] | Collection of tags associated with message | Yes |

## Example Query

### Basic Message Information

```graphql
query GetMessage($messageId: String!) {
  phisherMessage(id: $messageId) {
    id
    subject
    from
    reportedBy
    category
    severity
    actionStatus
    pipelineStatus
  }
}
```

### Detailed Message with Analysis

```graphql
query GetDetailedMessage($messageId: String!) {
  phisherMessage(id: $messageId) {
    id
    subject
    from
    reportedBy
    category
    severity
    actionStatus
    pipelineStatus
    
    # Attachments with scan status
    attachments(status: SCANNED) {
      filename
      contentType
      scanStatus
      threatFound
    }
    
    # Links with analysis
    links(status: ANALYZED) {
      url
      scanStatus
      reputation
      category
    }
    
    # Comments and workflow
    comments {
      id
      body
      createdAt
      createdBy
    }
    
    # Applied rules
    rules {
      id
      name
      description
      action
    }
    
    # Tags
    tags {
      id
      name
      type
    }
  }
}
```

### Message Headers and Technical Details

```graphql
query GetMessageHeaders($messageId: String!) {
  phisherMessage(id: $messageId) {
    id
    subject
    
    # Email headers
    headers {
      name
      value
    }
    
    # Raw message access
    rawUrl
    
    # PhishML analysis
    phishmlReport
    
    # Processing events
    events {
      id
      type
      timestamp
      description
      metadata
    }
  }
}
```

## Variables Example

```json
{
  "messageId": "00a43d65-5802-4df6-9c3c-f7d2024ddb0b"
}
```

## Response Example

```json
{
  "data": {
    "phisherMessage": {
      "id": "00a43d65-5802-4df6-9c3c-f7d2024ddb0b",
      "subject": "Urgent: Account Verification Required",
      "from": "noreply@suspicious-domain.com",
      "reportedBy": "user@company.com",
      "category": "THREAT",
      "severity": "HIGH",
      "actionStatus": "RESOLVED",
      "pipelineStatus": "PROCESSED",
      "attachments": [],
      "links": [
        {
          "url": "https://suspicious-domain.com/verify",
          "scanStatus": "MALICIOUS",
          "reputation": "BAD",
          "category": "PHISHING"
        }
      ],
      "comments": [
        {
          "id": "comment-123",
          "body": "Confirmed phishing attempt - blocked domain",
          "createdAt": "2024-01-15T10:30:00Z",
          "createdBy": "security-analyst@company.com"
        }
      ],
      "tags": [
        {
          "id": "tag-456",
          "name": "PHISHING",
          "type": "THREAT_TYPE"
        }
      ]
    }
  }
}
```

## Use Cases

### Security Analysis
- Retrieve detailed information about reported threats
- Analyze message content and attachments
- Review applied security rules and their outcomes

### Incident Response
- Get complete context for security incidents
- Access raw message data for forensic analysis
- Track resolution workflow and comments

### Compliance and Auditing
- Document security event details
- Track message processing and decisions
- Generate reports on threat handling

## Error Handling

### Message Not Found
```json
{
  "data": {
    "phisherMessage": null
  },
  "errors": [
    {
      "message": "Message not found",
      "path": ["phisherMessage"]
    }
  ]
}
```

### Invalid Message ID
```json
{
  "errors": [
    {
      "message": "Invalid message ID format",
      "path": ["phisherMessage"]
    }
  ]
}
```

## Related Queries

- [phisherMessages](query-phisher-messages.md) - Query multiple messages
- [phisherRule](query-phisher-rule.md) - Query specific rules
- [phisherRules](query-phisher-rules.md) - Query multiple rules
