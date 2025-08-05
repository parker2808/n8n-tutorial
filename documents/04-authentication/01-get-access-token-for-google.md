# Get Google API Access Token for N8N

## Overview

This guide provides step-by-step instructions for obtaining Google API access tokens that can be used in N8N workflows for services like Gmail, Google Sheets, Google Drive, and Google Calendar.

## Prerequisites

Before starting, ensure you have:

- A Google account
- Basic understanding of API authentication concepts
- N8N instance running

## Step 1: Create a Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Click "Select a project" → "New Project"
3. Enter a project name (e.g., "N8N Integration")
4. Click "Create"

## Step 2: Enable Required APIs

1. In your project, go to "APIs & Services" → "Library"
2. Search and enable the APIs you need:
   - **Gmail API** - For email automation
   - **Google Sheets API** - For spreadsheet operations
   - **Google Drive API** - For file management
   - **Google Calendar API** - For calendar automation

### To enable an API:

1. Search for the API name in the library
2. Click on the API
3. Click "Enable"

## Step 3: Create OAuth 2.0 Credentials

1. Go to "APIs & Services" → "Credentials"
2. Click "Create Credentials" → "OAuth 2.0 Client IDs"
3. If prompted, configure the OAuth consent screen first:
   - Choose "External" user type
   - Fill in app name, user support email, and developer contact
   - Add scopes for the APIs you'll use
   - Add test users if needed

### Create OAuth Client ID:

1. Choose application type:
   - **Desktop application** - For local development
   - **Web application** - For production use
2. Fill in the required information:
   - Name: "N8N Google Integration"
   - Authorized redirect URIs (for web apps):
     - `https://developers.google.com/oauthplayground/`
     - `http://localhost:3000/callback`
3. Click "Create"
4. Download the JSON credentials file

## Step 4: Generate Access Token

### Using Google OAuth 2.0 Playground

1. Visit [Google OAuth 2.0 Playground](https://developers.google.com/oauthplayground/)
2. Click the settings icon (⚙️) in the top right
3. Check "Use your own OAuth credentials"
4. Enter your Client ID and Client Secret from the downloaded JSON file
5. Click "Close"

### Select Required Scopes

Choose the scopes you need for your workflows:

- **Gmail**: `https://www.googleapis.com/auth/gmail.readonly` (read) or `https://www.googleapis.com/auth/gmail.modify` (read/write)
- **Google Sheets**: `https://www.googleapis.com/auth/spreadsheets` or `https://www.googleapis.com/auth/spreadsheets.readonly`
- **Google Drive**: `https://www.googleapis.com/auth/drive` or `https://www.googleapis.com/auth/drive.readonly`
- **Google Calendar**: `https://www.googleapis.com/auth/calendar` or `https://www.googleapis.com/auth/calendar.readonly`

### Generate Token

1. Select the scopes you need
2. Click "Authorize APIs"
3. Sign in with your Google account
4. Grant permissions to your app
5. Click "Exchange authorization code for tokens"
6. Copy the access token

## Step 5: Configure in N8N

### Add Google OAuth2 Credential

1. In N8N, go to Settings → Credentials
2. Click "Add Credential"
3. Search for "Google OAuth2" and select it
4. Fill in the credential details:
   - **Name**: "Google API Access"
   - **Client ID**: Your OAuth client ID
   - **Client Secret**: Your OAuth client secret
   - **Scope**: The scopes you need (space-separated)
   - **Access Token**: The token you generated
5. Click "Save"

### Test the Connection

1. Create a new workflow
2. Add a Google service node (e.g., Gmail, Google Sheets)
3. Select your credential
4. Test the connection

## Security Best Practices

### Token Management

1. **Never commit tokens to version control**
2. Store tokens securely in N8N's credential management
3. Rotate tokens regularly (Google tokens expire)
4. Use the minimum required permissions

### Environment Variables

Create a `.env` file for local development:

```bash
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
GOOGLE_ACCESS_TOKEN=your_google_access_token
```

## Troubleshooting

### Common Issues

1. **"Invalid Credentials"**

   - Verify Client ID and Secret are correct
   - Check that the OAuth consent screen is configured

2. **"Token Expired"**

   - Generate a new access token
   - Google tokens typically expire after 1 hour

3. **"Insufficient Permissions"**

   - Check that the required APIs are enabled
   - Verify the OAuth scopes are correct

4. **"Redirect URI Mismatch"**
   - Ensure redirect URIs in Google Cloud Console match your setup

### Debug Steps

1. Check N8N logs for authentication errors
2. Test API calls using Google's API Explorer
3. Verify token validity using curl:
   ```bash
   curl -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
        https://www.googleapis.com/oauth2/v1/userinfo
   ```

## Next Steps

Once you have successfully configured Google API access:

1. **Test API Connections**: Verify each Google service can be accessed
2. **Create Workflows**: Start building N8N workflows using Google services
3. **Monitor Usage**: Set up monitoring for API rate limits
4. **Proceed to Next Platform**: Continue with [LinkedIn API Setup](./02-get-access-token-for-linkedin.md) or [Facebook API Setup](./03-get-access-token-for-facebook.md)

## Related Files

- [Main Authentication Guide](./get-access-token.md) - Overview of all platforms
- [LinkedIn API Setup](./02-get-access-token-for-linkedin.md) - LinkedIn authentication
- [Facebook API Setup](./03-get-access-token-for-facebook.md) - Facebook authentication
- [Create N8N Workflow](../05-workflows/01-create-n8n-workflow.md) - Next step in the workflow

## Additional Resources

- [Google OAuth 2.0 Documentation](https://developers.google.com/identity/protocols/oauth2)
- [Google APIs Explorer](https://developers.google.com/apis-explorer/)
- [N8N Google Integrations](https://docs.n8n.io/integrations/nodes/n8n-nodes-base.google/)
- [Google Cloud Console](https://console.cloud.google.com/)
