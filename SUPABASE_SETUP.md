# Supabase Setup for Central Signature Tracking

This guide will help you set up a free Supabase database to track all signatures centrally.

## Quick Setup (5 minutes)

### 1. Create a Supabase Account

1. Go to [https://supabase.com](https://supabase.com)
2. Click "Start your project" and sign in with GitHub
3. Create a new project:
   - Name: `sensos-proposal-signatures`
   - Database Password: (save this securely)
   - Region: Choose closest to you
   - Click "Create new project"

### 2. Create the Signatures Table

1. In your Supabase dashboard, go to **Table Editor** (left sidebar)
2. Click **"New table"**
3. Configure the table:
   - **Name**: `signatures`
   - **Enable Row Level Security (RLS)**: UNCHECK this for now (we'll enable it in step 3)
4. Add these columns:

| Column Name | Type | Default Value | Primary | Nullable |
|------------|------|---------------|---------|----------|
| id | int8 | (auto) | ✓ | ✗ |
| created_at | timestamptz | now() | | ✗ |
| name | text | | | ✗ |
| email | text | | | ✗ |
| title | text | | | ✓ |
| company | text | | | ✓ |
| signed_at | timestamptz | | | ✗ |
| integrity_hash | text | | | ✗ |
| sow_version | text | | | ✗ |

5. Click **Save**

### 3. Set Up Security Policies

1. Go to **Authentication** → **Policies** (left sidebar)
2. Find your `signatures` table
3. Click **"New Policy"**
4. Create two policies:

**Policy 1: Allow Anyone to INSERT**
```sql
CREATE POLICY "Allow public inserts"
ON signatures
FOR INSERT
TO public
WITH CHECK (true);
```

**Policy 2: Allow Anyone to SELECT**
```sql
CREATE POLICY "Allow public reads"
ON signatures
FOR SELECT
TO public
USING (true);
```

5. Now enable RLS: Go back to **Table Editor** → click on `signatures` table → Settings → Enable RLS

### 4. Get Your API Keys

1. Go to **Settings** → **API** (left sidebar)
2. You'll see two values:
   - **Project URL**: Something like `https://xxxxx.supabase.co`
   - **anon public key**: Long string starting with `eyJ...`

### 5. Update Your Website

Open `index.html` and find this section around line 140:

```javascript
// --- SUPABASE SIGNATURE TRACKING ---
const SUPABASE_URL = 'https://xplhtqncuwvoxaywzrlo.supabase.co';
const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...';
```

Replace with your actual values:
```javascript
const SUPABASE_URL = 'YOUR_PROJECT_URL_HERE';
const SUPABASE_ANON_KEY = 'YOUR_ANON_KEY_HERE';
```

### 6. Deploy and Test

1. Save your changes and deploy to Vercel
2. Open the website and sign the agreement
3. Check your Supabase dashboard → Table Editor → `signatures` to see the new entry!

## Features Now Available

✅ **Central Tracking** - All signatures stored in one database  
✅ **Real-time Updates** - Signature list refreshes every 30 seconds  
✅ **Multiple Signers** - No limit on number of signatures  
✅ **Visible to All** - Anyone viewing the proposal can see who signed  
✅ **Secure** - Each signature has a cryptographic integrity hash  

## View Signatures

The signature list will appear on the main page in the left sidebar, showing:
- Name
- Title & Company
- Email
- Timestamp
- Total count

## Troubleshooting

**Signatures not appearing?**
- Check browser console for errors
- Verify your Supabase URL and API key are correct
- Ensure RLS policies are set up correctly

**"Database not available" error?**
- Make sure the Supabase script is loading (check browser console)
- Verify your API keys are correct

**Need help?**
- Supabase Discord: https://discord.supabase.com
- Documentation: https://supabase.com/docs

## Cost

Supabase free tier includes:
- 500MB database
- 1GB file storage
- 50MB file uploads
- 2GB bandwidth
- 50,000 monthly active users

This is more than enough for signature tracking! 🎉
