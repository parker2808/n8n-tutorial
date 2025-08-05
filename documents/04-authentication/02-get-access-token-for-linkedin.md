# Get LinkedIn API Access Token for N8N

## Overview

This guide provides step-by-step instructions for obtaining LinkedIn API access tokens that can be used in N8N workflows for LinkedIn marketing, networking automation, and social media management.

## Prerequisites

Before starting, ensure you have:

- A LinkedIn account
- A LinkedIn company page (recommended)
- Basic understanding of API authentication concepts
- N8N instance running

## Step 1: Create a LinkedIn App

1. Go to [LinkedIn Developers](https://www.linkedin.com/developers/)
2. Click "Create App"
3. Fill in the app details:
   - **App name**: "N8N LinkedIn Integration"
   - **LinkedIn Page**: Select your company page (or create one)
   - **App logo**: Upload a logo for your app
   - **App description**: Brief description of your app's purpose
4. Click "Create App"

## Step 2: Configure OAuth 2.0 Settings

1. In your app dashboard, go to the "Auth" tab
2. Under "OAuth 2.0 settings", add redirect URLs:
   - `https://developers.google.com/oauthplayground/`
   - `http://localhost:3000/callback`
   - `https://your-domain.com/callback` (for production)
3. Click "Save"

### Configure App Permissions

1. Go to the "Products" tab
2. Request access to the products you need:
   - **Sign In with LinkedIn** - Basic profile access
   - **Marketing Developer Platform** - For advertising features
   - **Share on LinkedIn** - For posting content
   - **LinkedIn Learning** - For learning content (if needed)

## Step 3: Get Client Credentials

1. In your app dashboard, go to the "Auth" tab
2. Note down your credentials:
   - **Client ID**: Your app's unique identifier
   - **Client Secret**: Your app's secret key (keep this secure)

### Store Credentials Securely

Create a secure file to store your credentials (see `env/linkedin/client_secret_key.json`):

```json
{
  "client_id": "your_linkedin_client_id",
  "client_secret": "your_linkedin_client_secret"
}
```

## Step 4: Generate Access Token

### Method 1: Using LinkedIn OAuth 2.0 Flow

1. Construct the authorization URL:

   ```
   https://www.linkedin.com/oauth/v2/authorization?response_type=code&client_id=YOUR_CLIENT_ID&redirect_uri=https://developers.google.com/oauthplayground/&scope=r_liteprofile%20r_emailaddress%20w_member_social
   ```

2. Replace `YOUR_CLIENT_ID` with your actual Client ID

3. Open the URL in your browser

4. Sign in to LinkedIn and authorize your app

5. Copy the authorization code from the redirect URL

### Method 2: Using OAuth Playground

1. Visit [Google OAuth 2.0 Playground](https://developers.google.com/oauthplayground/)
2. Click the settings icon (⚙️) in the top right
3. Check "Use your own OAuth credentials"
4. Enter your LinkedIn Client ID and Client Secret
5. Click "Close"

### Exchange Code for Token

Use the authorization code to get an access token:

```bash
curl -X POST https://www.linkedin.com/oauth/v2/accessToken \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "grant_type=authorization_code&code=AUTHORIZATION_CODE&client_id=YOUR_CLIENT_ID&client_secret=YOUR_CLIENT_SECRET&redirect_uri=https://developers.google.com/oauthplayground/"
```

Replace:

- `AUTHORIZATION_CODE` with the code you received
- `YOUR_CLIENT_ID` with your LinkedIn Client ID
- `YOUR_CLIENT_SECRET` with your LinkedIn Client Secret

## Step 5: Configure in N8N

### Add LinkedIn OAuth2 Credential

1. In N8N, go to Settings → Credentials
2. Click "Add Credential"
3. Search for "LinkedIn OAuth2" and select it
4. Fill in the credential details:
   - **Name**: "LinkedIn API Access"
   - **Client ID**: Your LinkedIn Client ID
   - **Client Secret**: Your LinkedIn Client Secret
   - **Access Token**: The token you generated
5. Click "Save"

### Test the Connection

1. Create a new workflow
2. Add a LinkedIn node (e.g., LinkedIn Trigger, LinkedIn)
3. Select your credential
4. Test the connection

## Available LinkedIn Scopes

Choose the scopes you need for your workflows:

- **`r_liteprofile`** - Read basic profile information
- **`r_emailaddress`** - Read email address
- **`w_member_social`** - Post, comment, and like on LinkedIn
- **`r_organization_social`** - Read organization posts
- **`w_organization_social`** - Post on organization pages
- **`r_ads`** - Read advertising data
- **`w_ads`** - Write advertising data

## Security Best Practices

### Token Management

1. **Never commit tokens to version control**
2. Store tokens securely in N8N's credential management
3. Rotate tokens regularly
4. Use the minimum required permissions

### Environment Variables

Create a `.env` file for local development:

```bash
LINKEDIN_CLIENT_ID=your_linkedin_client_id
LINKEDIN_CLIENT_SECRET=your_linkedin_client_secret
LINKEDIN_ACCESS_TOKEN=your_linkedin_access_token
```

## Troubleshooting

### Common Issues

1. **"Invalid Client ID"**

   - Verify your Client ID is correct
   - Check that your app is properly configured

2. **"Redirect URI Mismatch"**

   - Ensure redirect URIs in LinkedIn app match your setup
   - Check for trailing slashes or protocol differences

3. **"Insufficient Permissions"**

   - Verify the required scopes are included in your authorization request
   - Check that your app has been approved for the requested permissions

4. **"Token Expired"**
   - LinkedIn tokens can expire; generate a new one
   - Consider implementing token refresh logic

### Debug Steps

1. Check N8N logs for authentication errors
2. Test API calls using LinkedIn's API Explorer
3. Verify token validity using curl:
   ```bash
   curl -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
        https://api.linkedin.com/v2/me
   ```

## Next Steps

Once you have successfully configured LinkedIn API access:

1. **Test API Connections**: Verify LinkedIn services can be accessed
2. **Create Workflows**: Start building N8N workflows using LinkedIn
3. **Monitor Usage**: Set up monitoring for API rate limits
4. **Proceed to Next Platform**: Continue with [Google API Setup](./01-get-access-token-for-google.md) or [Facebook API Setup](./03-get-access-token-for-facebook.md)

## Related Files

- [Main Authentication Guide](./get-access-token.md) - Overview of all platforms
- [Google API Setup](./01-get-access-token-for-google.md) - Google authentication
- [Facebook API Setup](./03-get-access-token-for-facebook.md) - Facebook authentication
- [Create N8N Workflow](../05-workflows/01-create-n8n-workflow.md) - Next step in the workflow
- `env/linkedin/client_secret_key.json` - LinkedIn API credentials

## Additional Resources

- [LinkedIn API Documentation](https://developer.linkedin.com/docs)
- [LinkedIn OAuth 2.0 Guide](https://developer.linkedin.com/docs/oauth2)
- [N8N LinkedIn Integrations](https://docs.n8n.io/integrations/nodes/n8n-nodes-base.linkedin/)
- [LinkedIn Developers Portal](https://www.linkedin.com/developers/)
