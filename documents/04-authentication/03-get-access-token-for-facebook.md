# Get Facebook API Access Token for N8N

## Overview

This guide provides step-by-step instructions for obtaining Facebook API access tokens that can be used in N8N workflows for Facebook marketing, social media automation, and business page management.

## Prerequisites

Before starting, ensure you have:

- A Facebook account
- A Facebook Business Page (recommended)
- Basic understanding of API authentication concepts
- N8N instance running

## Step 1: Create a Facebook App

1. Go to [Facebook Developers](https://developers.facebook.com/)
2. Click "Create App"
3. Choose the app type:
   - **Business** - Recommended for marketing and business automation
   - **Consumer** - For personal use
   - **Other** - For specific use cases
4. Fill in the app details:
   - **App name**: "N8N Facebook Integration"
   - **Contact email**: Your email address
   - **Business account**: Select your business account (if applicable)
5. Click "Create App"

## Step 2: Configure App Settings

1. In your app dashboard, go to "Settings" → "Basic"
2. Note down your credentials:
   - **App ID**: Your app's unique identifier
   - **App Secret**: Your app's secret key (keep this secure)
3. Add your domain to "App Domains":
   - `localhost` (for development)
   - `your-domain.com` (for production)
4. Click "Save Changes"

### Configure Privacy Policy

1. Go to "Settings" → "Basic"
2. Add your privacy policy URL (required for production)
3. Add your terms of service URL (optional but recommended)

## Step 3: Add Required Products

1. Go to the "Products" tab
2. Add the products you need for your workflows:

### Essential Products

- **Facebook Login** - For user authentication
- **Pages API** - For managing Facebook pages
- **Marketing API** - For advertising and insights
- **Instagram Basic Display** - For Instagram integration (if needed)

### To add a product:

1. Click "Set Up" next to the product
2. Follow the configuration steps
3. Complete the setup process

## Step 4: Configure OAuth Settings

1. Go to "Facebook Login" → "Settings"
2. Add Valid OAuth Redirect URIs:
   - `https://developers.google.com/oauthplayground/`
   - `http://localhost:3000/callback`
   - `https://your-domain.com/callback` (for production)
3. Save changes

### Configure App Permissions

1. Go to "App Review" → "Permissions and Features"
2. Request the permissions you need:
   - **pages_read_engagement** - Read page insights
   - **pages_manage_posts** - Post on pages
   - **pages_show_list** - Access page information
   - **ads_read** - Read advertising data
   - **ads_management** - Manage advertising

## Step 5: Generate Access Token

### Method 1: Using Graph API Explorer

1. Go to [Graph API Explorer](https://developers.facebook.com/tools/explorer/)
2. Select your app from the dropdown
3. Click "Generate Access Token"
4. Grant the necessary permissions
5. Copy the access token

### Method 2: Using OAuth Flow

1. Construct the authorization URL:

   ```
   https://www.facebook.com/v18.0/dialog/oauth?client_id=YOUR_APP_ID&redirect_uri=https://developers.google.com/oauthplayground/&scope=pages_read_engagement,pages_manage_posts
   ```

2. Replace `YOUR_APP_ID` with your actual App ID

3. Open the URL in your browser

4. Sign in to Facebook and authorize your app

5. Copy the authorization code from the redirect URL

### Exchange Code for Token

Use the authorization code to get an access token:

```bash
curl -X GET "https://graph.facebook.com/v18.0/oauth/access_token?client_id=YOUR_APP_ID&client_secret=YOUR_APP_SECRET&code=AUTHORIZATION_CODE&redirect_uri=https://developers.google.com/oauthplayground/"
```

Replace:

- `YOUR_APP_ID` with your Facebook App ID
- `YOUR_APP_SECRET` with your Facebook App Secret
- `AUTHORIZATION_CODE` with the code you received

## Step 6: Configure in N8N

### Add Facebook OAuth2 Credential

1. In N8N, go to Settings → Credentials
2. Click "Add Credential"
3. Search for "Facebook OAuth2" and select it
4. Fill in the credential details:
   - **Name**: "Facebook API Access"
   - **App ID**: Your Facebook App ID
   - **App Secret**: Your Facebook App Secret
   - **Access Token**: The token you generated
5. Click "Save"

### Test the Connection

1. Create a new workflow
2. Add a Facebook node (e.g., Facebook Trigger, Facebook)
3. Select your credential
4. Test the connection

## Available Facebook Permissions

Choose the permissions you need for your workflows:

### Page Management

- **`pages_read_engagement`** - Read page insights and engagement
- **`pages_manage_posts`** - Post on pages
- **`pages_show_list`** - Access page information
- **`pages_manage_metadata`** - Manage page settings

### Advertising

- **`ads_read`** - Read advertising data
- **`ads_management`** - Manage advertising campaigns
- **`business_management`** - Manage business accounts

### User Data

- **`email`** - Access user email
- **`public_profile`** - Access public profile information

## Security Best Practices

### Token Management

1. **Never commit tokens to version control**
2. Store tokens securely in N8N's credential management
3. Rotate tokens regularly
4. Use the minimum required permissions

### Environment Variables

Create a `.env` file for local development:

```bash
FACEBOOK_APP_ID=your_facebook_app_id
FACEBOOK_APP_SECRET=your_facebook_app_secret
FACEBOOK_ACCESS_TOKEN=your_facebook_access_token
```

## Troubleshooting

### Common Issues

1. **"Invalid App ID"**

   - Verify your App ID is correct
   - Check that your app is properly configured

2. **"Redirect URI Mismatch"**

   - Ensure redirect URIs in Facebook app match your setup
   - Check for trailing slashes or protocol differences

3. **"Insufficient Permissions"**

   - Verify the required permissions are included in your authorization request
   - Check that your app has been approved for the requested permissions

4. **"Token Expired"**

   - Facebook tokens can expire; generate a new one
   - Consider implementing token refresh logic

5. **"App Review Required"**
   - Some permissions require Facebook app review
   - Use development mode for testing

### Debug Steps

1. Check N8N logs for authentication errors
2. Test API calls using Facebook's Graph API Explorer
3. Verify token validity using curl:
   ```bash
   curl -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
        https://graph.facebook.com/v18.0/me
   ```

## Next Steps

Once you have successfully configured Facebook API access:

1. **Test API Connections**: Verify Facebook services can be accessed
2. **Create Workflows**: Start building N8N workflows using Facebook
3. **Monitor Usage**: Set up monitoring for API rate limits
4. **Proceed to Next Platform**: Continue with [Google API Setup](./01-get-access-token-for-google.md) or [LinkedIn API Setup](./02-get-access-token-for-linkedin.md)

## Related Files

- [Main Authentication Guide](./get-access-token.md) - Overview of all platforms
- [Google API Setup](./01-get-access-token-for-google.md) - Google authentication
- [LinkedIn API Setup](./02-get-access-token-for-linkedin.md) - LinkedIn authentication
- [Create N8N Workflow](../05-workflows/01-create-n8n-workflow.md) - Next step in the workflow

## Additional Resources

- [Facebook Graph API Documentation](https://developers.facebook.com/docs/graph-api)
- [Facebook OAuth 2.0 Guide](https://developers.facebook.com/docs/facebook-login/security)
- [N8N Facebook Integrations](https://docs.n8n.io/integrations/nodes/n8n-nodes-base.facebook/)
- [Facebook Developers Portal](https://developers.facebook.com/)
- [Graph API Explorer](https://developers.facebook.com/tools/explorer/)
