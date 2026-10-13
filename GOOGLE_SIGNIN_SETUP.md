# Ski Ready — Enable Google sign-in alongside email links

The **Continue with Google** button is already present in `index.html`. It calls Supabase Auth's `signInWithOAuth({provider:'google'})`. Email magic links remain enabled.

## 1. Create a Google OAuth app

1. Sign into [Google Cloud Console](https://console.cloud.google.com/) with the Google account that will own the integration.
2. Create/select a Google Cloud project for Ski Ready.
3. Open [Google Auth Platform](https://console.cloud.google.com/auth/overview).
4. Configure **Branding** and **Audience**. For your own account while testing, choose **External**, set **Testing**, and add your Google account as a test user if required. Before offering the app publicly, check publication/verification requirements.
5. Create a new OAuth client at [Clients](https://console.cloud.google.com/auth/clients) with application type **Web application**.
6. Under **Authorized JavaScript origins**, add exactly:
   `https://callumcr27.github.io`
7. Under **Authorized redirect URIs**, add exactly:
   `https://qxngltvddsgywaoyfuup.supabase.co/auth/v1/callback`
8. Save the OAuth **Client ID** and **Client secret**. **Never put the secret in a GitHub repo, HTML file, issue or public chat.**

## 2. Enable Google in Supabase

1. Visit [Supabase Authentication → Google provider](https://supabase.com/dashboard/project/qxngltvddsgywaoyfuup/auth/providers?provider=Google).
2. Enable Google sign-in.
3. Paste the **Client ID** and **Client Secret** from Google Cloud into the protected Supabase provider settings. Save.
4. Confirm [Supabase redirect URLs](https://supabase.com/dashboard/project/qxngltvddsgywaoyfuup/auth/url-configuration) include:
   `https://callumcr27.github.io/Ski-ready/`

## 3. Test on iPhone and Mac

1. Open [Ski Ready](https://callumcr27.github.io/Ski-ready/) in Safari.
2. In **Cloud sync**, choose **Continue with Google** and follow the Google sign-in.
3. You should return to the app and see a signed-in state. Choose **Start sync using this device** on your current phone only if it holds your desired records.
4. On a second device, sign in with the same Google account and choose **Use cloud copy** when prompted.
5. Confirm a small test drink or workout appears on both devices.

**Important:** Export a JSON backup before choosing which copy to upload. If you have an existing email-link account, use the **same verified email address** with Google to permit Supabase's automatic identity linking. Using a different Google account may create a separate empty account and separate cloud records. Don't overwrite populated cloud data with an empty local copy.

## Email-link sign-in stays available

Supabase's default email service is intentionally rate-limited. Google sign-in avoids the email-link send limit, but does not change that limit for email sign-in. To offer email login reliably at scale, configure a trusted custom SMTP provider in [Supabase Auth SMTP settings](https://supabase.com/dashboard/project/qxngltvddsgywaoyfuup/auth/smtp).

Reference: [Supabase Sign in with Google](https://supabase.com/docs/guides/auth/social-login/auth-google) and [Identity linking](https://supabase.com/docs/guides/auth/auth-identity-linking).
