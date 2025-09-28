# PhishER GraphQL API Base URLs

## Overview

When submitting API requests, you will need to use the correct base URL based on your account's server location.

## Regional Base URLs

The PhishER GraphQL API is available across multiple regions. Use the base URL that corresponds to your account's server location:

| Region | Server Location | Base URL |
|--------|----------------|----------|
| **US** | training.knowbe4.com | `https://training.knowbe4.com/graphql` |
| **EU** | eu.knowbe4.com | `https://eu.knowbe4.com/graphql` |
| **CA** | ca.knowbe4.com | `https://ca.knowbe4.com/graphql` |
| **UK** | uk.knowbe4.com | `https://uk.knowbe4.com/graphql` |
| **DE** | de.knowbe4.com | `https://de.knowbe4.com/graphql` |

## Determining Your Server Location

To determine which base URL to use:

1. **Check your KnowBe4 login URL**: The domain you use to access your KnowBe4 console indicates your server region
2. **US Accounts**: If you log in at `training.knowbe4.com`, use the US base URL
3. **EU Accounts**: If you log in at `eu.knowbe4.com`, use the EU base URL
4. **CA Accounts**: If you log in at `ca.knowbe4.com`, use the CA base URL
5. **UK Accounts**: If you log in at `uk.knowbe4.com`, use the UK base URL
6. **DE Accounts**: If you log in at `de.knowbe4.com`, use the DE base URL

## API Endpoint Structure

All GraphQL requests should be sent as POST requests to the `/graphql` endpoint of your regional base URL.

### Example Request Structure

```bash
POST https://training.knowbe4.com/graphql
Content-Type: application/json
Authorization: Bearer YOUR_API_TOKEN

{
  "query": "your GraphQL query here"
}
```

## Important Notes

- Always use HTTPS for API requests
- Ensure you're using the correct regional endpoint for your account
- The GraphQL endpoint is consistent across all regions (`/graphql`)
- API tokens are region-specific and will only work with the corresponding regional endpoint

## Next Steps

- Set up [Authentication](authentication.md) with your API token
- Review available [Queries](queries.md) and [Mutations](mutations.md)
- Explore the [Types](types.md) and [Inputs](inputs.md) available in the API
