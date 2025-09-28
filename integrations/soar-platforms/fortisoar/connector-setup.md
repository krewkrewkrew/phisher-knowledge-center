# KnowBe4 PhishER FortiSOAR Connector v1.0.1

## About the Connector

KnowBe4 PhishER helps your InfoSec and Security Operations team cut through the inbox noise and respond to the most dangerous threats more quickly.

This document provides information about the KnowBe4 PhishER Connector, which facilitates automated interactions with a KnowBe4 PhishER server using FortiSOAR™ playbooks. Add the KnowBe4 PhishER Connector as a step in FortiSOAR™ playbooks and perform automated operations with KnowBe4 PhishER.

## Version Information

| Component | Version |
|-----------|---------|
| **Connector Version** | 1.0.1 |
| **FortiSOAR™ Version Tested** | 7.6.0-5012 |
| **KnowBe4 PhishER Version Tested** | Cloud Setup |
| **Authored By** | Fortinet |
| **Certified** | Yes |

## Release Notes for Version 1.0.1

Following enhancements have been made to the KnowBe4 PhishER connector in version 1.0.1:

- Added a new action **Get Message By ID**
- Removed the parameter **Message ID** from the action **Get Messages**
- Fixed issues with **Get Messages** and **Update Message** actions to fetch and update records appropriately

## Installing the Connector

### Content Hub Installation

Use the Content Hub to install the connector. For the detailed procedure to install a connector, click [here](https://docs.fortinet.com/document/fortisoar/0.0.0/installing-a-connector-from-content-hub).

### Command Line Installation

You can also use the yum command as a root user to install the connector:

```bash
yum install cyops-connector-knowb4-phisher
```

## Prerequisites to Configuring the Connector

Before configuring the KnowBe4 PhishER connector, ensure the following prerequisites are met:

- You must have the credentials of KnowBe4 PhishER server to which you will connect and perform automated operations
- The FortiSOAR™ server should have outbound connectivity to port 443 on the KnowBe4 PhishER server

## Minimum Permissions Required

Not applicable - the connector uses the permissions associated with the provided API key.

## Configuring the Connector

For the procedure to configure a connector, click [here](https://docs.fortinet.com/document/fortisoar/0.0.0/configuring-a-connector).

### Configuration Parameters

In FortiSOAR™, on the Connectors page, click the **KnowBe4 PhishER** connector row (if you are in the **Grid** view on the Connectors page) and in the **Configurations** tab enter the required configuration details:

| Parameter | Description | Required |
|-----------|-------------|----------|
| **Server URL** | Specify the server URL to connect and perform automated operations | Yes |
| **API Key** | Specify the API key to access the endpoint to connect and perform the automated operations | Yes |
| **Verify SSL** | Specifies whether the SSL certificate for the server is to be verified. By default, this option is selected (set to `true`) | No |

### Server URL Examples

Based on your KnowBe4 account region, use the appropriate server URL:

| Region | Server URL |
|--------|------------|
| US | `https://training.knowbe4.com` |
| EU | `https://eu.knowbe4.com` |
| CA | `https://ca.knowbe4.com` |
| UK | `https://uk.knowbe4.com` |
| DE | `https://de.knowbe4.com` |

## Actions Supported by the Connector

The following automated operations can be included in playbooks and you can also use the annotations to access operations from FortiSOAR™ release 4.10.0 and onwards:

| Function | Description | Annotation and Category |
|----------|-------------|-------------------------|
| **Get Messages** | Retrieves a detailed list of messages based on the lucene search query, pagination, and other input parameters that you have specified | `get_message_list` Investigation |
| **Get Message by ID** | Retrieves a message's details based on the message ID that you have specified | `get_message_by_id` Investigation |
| **Update Message** | Updates a message based on the message ID, category, and other input parameters that you have specified | `update_message` Investigation |
| **Add Comment** | Adds a comment on a message based on the message ID and the comment that you have specified | `add_comment` Investigation |
| **Add Tags** | Adds tags to a message based on the message ID and the tag that you have specified | `add_tags` Investigation |
| **Remove Tags** | Removes tags from a message based on the message ID and the tag that you have specified | `remove_tags` Investigation |

## Action Details

### Get Messages

Retrieves a detailed list of messages based on search criteria and pagination parameters.

**Parameters:**
- **Lucene Query** (Optional): Search query using Lucene syntax
- **Limit** (Optional): Maximum number of messages to retrieve
- **Offset** (Optional): Number of messages to skip for pagination

### Get Message by ID

Retrieves detailed information about a specific message.

**Parameters:**
- **Message ID** (Required): Unique identifier of the message to retrieve

### Update Message

Updates the properties of a specific message.

**Parameters:**
- **Message ID** (Required): Unique identifier of the message to update
- **Category** (Optional): Message category (CLEAN, SPAM, THREAT, etc.)
- **Status** (Optional): Message status (RECEIVED, IN_REVIEW, RESOLVED)
- **Severity** (Optional): Message severity (LOW, MEDIUM, HIGH, CRITICAL)

### Add Comment

Adds a comment to a specific message.

**Parameters:**
- **Message ID** (Required): Unique identifier of the message
- **Comment** (Required): Comment text to add

### Add Tags

Adds tags to a specific message.

**Parameters:**
- **Message ID** (Required): Unique identifier of the message
- **Tags** (Required): Comma-separated list of tags to add

### Remove Tags

Removes tags from a specific message.

**Parameters:**
- **Message ID** (Required): Unique identifier of the message
- **Tags** (Required): Comma-separated list of tags to remove

## Playbook Integration Examples

### Automated Threat Response Playbook

```yaml
# Example playbook step for automated threat categorization
- name: "Categorize High-Risk Message"
  action: "update_message"
  parameters:
    message_id: "{{ message.id }}"
    category: "THREAT"
    severity: "HIGH"
    status: "IN_REVIEW"

- name: "Add Threat Intelligence Tags"
  action: "add_tags"
  parameters:
    message_id: "{{ message.id }}"
    tags: "PHISHING,HIGH_PRIORITY,AUTO_DETECTED"

- name: "Add Analysis Comment"
  action: "add_comment"
  parameters:
    message_id: "{{ message.id }}"
    comment: "Automatically categorized as threat based on URL reputation analysis"
```

### Message Investigation Workflow

```yaml
# Example playbook for message investigation
- name: "Get Message Details"
  action: "get_message_by_id"
  parameters:
    message_id: "{{ incident.message_id }}"
  
- name: "Search Related Messages"
  action: "get_message_list"
  parameters:
    lucene_query: "from:{{ message.from }} AND category:THREAT"
    limit: 50
```

## Error Handling

The connector provides detailed error messages for common issues:

- **Authentication Errors**: Invalid API key or server URL
- **Permission Errors**: Insufficient permissions for the requested operation
- **Not Found Errors**: Message ID does not exist
- **Validation Errors**: Invalid parameter values or formats

## Best Practices

### Security
- Store API keys securely using FortiSOAR's credential management
- Use SSL verification in production environments
- Regularly rotate API keys

### Performance
- Use appropriate pagination limits for large result sets
- Implement proper error handling in playbooks
- Cache frequently accessed message data when appropriate

### Workflow Design
- Combine multiple actions in logical sequences
- Use conditional logic based on message properties
- Implement proper logging and audit trails

## Troubleshooting

### Common Issues

1. **Connection Timeout**: Check network connectivity and firewall rules
2. **SSL Certificate Errors**: Verify SSL settings and certificate validity
3. **API Rate Limiting**: Implement appropriate delays between requests
4. **Invalid Message IDs**: Ensure message IDs are valid and accessible

### Debug Information

Enable debug logging in FortiSOAR to capture detailed API interactions and troubleshoot integration issues.

## Related Documentation

- [KnowBe4 PhishER API Documentation](../api-docs/introduction.md)
- [FortiSOAR Connector Development Guide](https://docs.fortinet.com/document/fortisoar/0.0.0/connector-development-guide)
- [FortiSOAR Playbook Development](https://docs.fortinet.com/document/fortisoar/0.0.0/playbook-development-guide)
