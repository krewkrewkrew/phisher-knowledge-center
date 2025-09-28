# PhishER GraphQL API Introduction

## Overview

KnowBe4's APIs are GraphQL-based that allow you to evaluate all of the suspicious emails that make it through to your users' inboxes. With PhishER, you can identify potential threats and strengthen your security measures and defense-in-depth plan. Data is returned in a JSON structure by default--no additional parameter is needed.

## Terms of Use

By using KnowBe4's APIs, you agree to our [Terms of Use](https://www.knowbe4.com/terms-of-use).

## API Architecture

Our APIs use resource-oriented URLs for requests and HTTP response codes for error handling. HTTP features, such as HTTP authentication and HTTP verbs, are built-in and understood by standard HTTP clients.

## Important Notes

⚠️ **Important**: Deletions are permanent and can't be undone.

## Data Format

- Data is returned in JSON structure by default
- No additional parameters needed for JSON response format
- GraphQL-based API architecture
- Resource-oriented URL structure

## Authentication

The PhishER API requires proper authentication tokens. See the Authentication section for detailed information on obtaining and using authorization tokens.

## Regional Endpoints

The API supports multiple regional endpoints:
- US (United States)
- EU (European Union) 
- CA (Canada)
- UK (United Kingdom)
- DE (Germany)

## Getting Started

To begin using the PhishER API:

1. Obtain an authorization token from your KnowBe4 account
2. Select the appropriate regional endpoint
3. Review the available queries and mutations
4. Test API calls using the interactive documentation

## Next Steps

- Review [Base URL](base-url.md) configuration
- Set up [Authentication](authentication.md)
- Explore available [Queries](queries.md) and [Mutations](mutations.md)
- Understand [Types](types.md), [Inputs](inputs.md), and [Enums](enums.md)
