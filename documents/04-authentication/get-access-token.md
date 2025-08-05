# Get Access Tokens for N8N Workflows

## Overview

This document provides an overview of obtaining access tokens from three major platforms that are commonly used in N8N workflows:

1. **Google APIs** - For Gmail, Google Sheets, Google Drive, and other Google services
2. **LinkedIn API** - For LinkedIn marketing and networking automation
3. **Facebook API** - For Facebook marketing and social media automation

## Quick Start Guide

For detailed step-by-step instructions, refer to the individual platform guides:

- **[Google API Setup](./01-get-access-token-for-google.md)** - Complete Google OAuth setup
- **[LinkedIn API Setup](./02-get-access-token-for-linkedin.md)** - Complete LinkedIn OAuth setup
- **[Facebook API Setup](./03-get-access-token-for-facebook.md)** - Complete Facebook OAuth setup

## Prerequisites

Before obtaining access tokens, ensure you have:

- A Google account (for Google APIs)
- A LinkedIn account (for LinkedIn API)
- A Facebook account (for Facebook API)
- Basic understanding of API authentication concepts
- N8N instance running

## Platform Comparison

| Platform     | Use Cases                                       | Key Features                           | Token Expiry         |
| ------------ | ----------------------------------------------- | -------------------------------------- | -------------------- |
| **Google**   | Email automation, Spreadsheets, File management | Gmail, Sheets, Drive, Calendar         | 1 hour (refreshable) |
| **LinkedIn** | Professional networking, Content marketing      | Profile management, Posting, Analytics | Varies (refreshable) |
| **Facebook** | Social media marketing, Business pages          | Page management, Advertising, Insights | Varies (refreshable) |

## Common Setup Steps

All platforms follow a similar OAuth 2.0 flow:

1. **Create Developer Account** - Register on the platform's developer portal
2. **Create Application** - Set up your app with basic information
3. **Configure OAuth Settings** - Add redirect URIs and permissions
4. **Generate Credentials** - Get Client ID and Client Secret
5. **Obtain Access Token** - Use OAuth flow to get tokens
6. **Configure in N8N** - Add credentials to N8N

## Security Best Practices

### Token Storage

1. **Never commit tokens to version control**
2. Store tokens in environment variables
3. Use N8N's credential management system
4. Rotate tokens regularly

### Access Control

1. Use the minimum required permissions
2. Regularly review and revoke unused tokens
3. Monitor API usage and set up alerts
4. Use service accounts when possible

### Environment Setup

Create a `.env` file (not committed to git):

```bash
# Google API
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
GOOGLE_ACCESS_TOKEN=your_google_access_token

# LinkedIn API
LINKEDIN_CLIENT_ID=your_linkedin_client_id
LINKEDIN_CLIENT_SECRET=your_linkedin_client_secret
LINKEDIN_ACCESS_TOKEN=your_linkedin_access_token

# Facebook API
FACEBOOK_APP_ID=your_facebook_app_id
FACEBOOK_APP_SECRET=your_facebook_app_secret
FACEBOOK_ACCESS_TOKEN=your_facebook_access_token
```

## Troubleshooting

### Common Issues Across Platforms

1. **Token Expired**: Refresh tokens or generate new ones
2. **Insufficient Permissions**: Check API scopes and app permissions
3. **Rate Limiting**: Implement proper error handling and retry logic
4. **Invalid Credentials**: Verify client IDs and secrets
5. **Redirect URI Mismatch**: Ensure URIs match exactly

### Debug Steps

1. Check N8N logs for authentication errors
2. Verify token validity using platform-specific tools:
   - **Google**: [OAuth Playground](https://developers.google.com/oauthplayground/)
   - **LinkedIn**: [API Explorer](https://developer.linkedin.com/docs/rest-api)
   - **Facebook**: [Graph API Explorer](https://developers.facebook.com/tools/explorer/)
3. Test API calls using curl or Postman
4. Review app settings and permissions

### Platform-Specific Issues

#### Google

- OAuth consent screen configuration required
- API quotas and rate limits
- Service account vs OAuth 2.0

#### LinkedIn

- App review process for certain permissions
- Company page requirements
- Marketing API access restrictions

#### Facebook

- App review required for production
- Business verification needed
- Page access token vs user access token

## Next Steps

Once you have obtained all necessary access tokens:

1. **Configure N8N Credentials**: Add all tokens to N8N's credential management
2. **Test API Connections**: Verify each service can be accessed
3. **Create Workflows**: Proceed to [Create N8N Workflow](../05-workflows/01-create-n8n-workflow.md)
4. **Monitor Usage**: Set up monitoring for API rate limits and errors

## Detailed Guides

### [Google API Setup](./01-get-access-token-for-google.md)

- Google Cloud Console setup
- OAuth 2.0 credential creation
- Gmail, Sheets, Drive, Calendar APIs
- Token generation and N8N configuration

### [LinkedIn API Setup](./02-get-access-token-for-linkedin.md)

- LinkedIn Developers app creation
- OAuth 2.0 configuration
- Marketing and social features
- Profile and page management

### [Facebook API Setup](./03-get-access-token-for-facebook.md)

- Facebook Developers app setup
- Graph API configuration
- Page and advertising features
- Business account integration

## Related Files

- `env/linkedin/client_secret_key.json` - LinkedIn API credentials
- `documents/04-authentication/01-get-access-token-for-google.md` - Detailed Google setup
- `documents/04-authentication/02-get-access-token-for-linkedin.md` - Detailed LinkedIn setup
- `documents/04-authentication/03-get-access-token-for-facebook.md` - Detailed Facebook setup

## Additional Resources

- [Google OAuth 2.0 Documentation](https://developers.google.com/identity/protocols/oauth2)
- [LinkedIn API Documentation](https://developer.linkedin.com/docs)
- [Facebook Graph API Documentation](https://developers.facebook.com/docs/graph-api)
- [N8N Credentials Documentation](https://docs.n8n.io/integrations/credentials/)
