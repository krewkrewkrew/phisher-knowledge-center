# PhishER GraphQL API Authentication

## Overview

Authenticate your account by including your secret API key in the request. You can access your PhishER Product API key and generate a new key if needed in your KnowBe4 Account Settings under the API section.

## API Key Management

### Accessing Your API Key

1. Log in to your KnowBe4 console
2. Navigate to **Account Settings**
3. Go to the **API** section
4. Locate your **PhishER Product API key**
5. Generate a new key if needed

### Security Best Practices

Your API keys provide access to the data within your KnowBe4 platform and should be kept private:

- **Keep API keys confidential**: Do not share your API key in publicly-accessible areas
- **Store securely**: Use environment variables or secure credential storage
- **Rotate regularly**: Generate new keys periodically for enhanced security
- **Monitor usage**: Track API key usage for suspicious activity

## Authentication Header

The PhishER Product API key should be included in all API requests to the server. The header should look like the following:

```
Authorization: Bearer <your_token>
```

⚠️ **Important**: You must replace `<your_token>` with your PhishER Product API key.

## Request Requirements

### HTTPS Only

All API requests must be made over HTTPS. Calls made over plain HTTP will fail.

### Authentication Required

API requests without authentication will also fail. Every request must include the proper Authorization header.

## Example Request

```bash
curl -X POST https://training.knowbe4.com/graphql \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_PHISHER_API_KEY" \
  -d '{
    "query": "query { messages(first: 10) { edges { node { id subject } } } }"
  }'
```

## Example with Different Programming Languages

### Python

```python
import requests
import json

url = "https://training.knowbe4.com/graphql"
headers = {
    "Content-Type": "application/json",
    "Authorization": "Bearer YOUR_PHISHER_API_KEY"
}

query = """
query {
  messages(first: 10) {
    edges {
      node {
        id
        subject
      }
    }
  }
}
"""

response = requests.post(url, headers=headers, json={"query": query})
data = response.json()
```

### JavaScript

```javascript
const fetch = require('node-fetch');

const url = 'https://training.knowbe4.com/graphql';
const headers = {
  'Content-Type': 'application/json',
  'Authorization': 'Bearer YOUR_PHISHER_API_KEY'
};

const query = `
  query {
    messages(first: 10) {
      edges {
        node {
          id
          subject
        }
      }
    }
  }
`;

fetch(url, {
  method: 'POST',
  headers: headers,
  body: JSON.stringify({ query: query })
})
.then(response => response.json())
.then(data => console.log(data));
```

### PowerShell

```powershell
$uri = "https://training.knowbe4.com/graphql"
$headers = @{
    "Content-Type" = "application/json"
    "Authorization" = "Bearer YOUR_PHISHER_API_KEY"
}

$query = @"
query {
  messages(first: 10) {
    edges {
      node {
        id
        subject
      }
    }
  }
}
"@

$body = @{
    query = $query
} | ConvertTo-Json

$response = Invoke-RestMethod -Uri $uri -Method POST -Headers $headers -Body $body
```

## Troubleshooting Authentication

### Common Issues

1. **401 Unauthorized**: Check that your API key is correct and properly formatted
2. **403 Forbidden**: Verify that your API key has the necessary permissions
3. **SSL/TLS Errors**: Ensure you're using HTTPS and have proper certificate validation

### Testing Authentication

Use a simple query to test your authentication setup:

```graphql
query {
  viewer {
    id
    email
  }
}
```

## Next Steps

- Review [Pagination](pagination.md) for handling large result sets
- Explore available [Queries](queries.md) and [Mutations](mutations.md)
- Understand the [Types](types.md) and [Inputs](inputs.md) available in the API
