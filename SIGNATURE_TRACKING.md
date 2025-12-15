# Central Signature Tracking - Quick Reference

## What Changed

Your proposal now has **central signature tracking** that works across all devices and browsers!

## New Features

1. **Signature Database** - All signatures saved to Supabase (cloud database)
2. **Live Signature List** - Shows who has signed (refreshes every 30s)
3. **Multiple Signatures** - No limits, anyone can sign multiple times
4. **Public Visibility** - Anyone viewing the proposal sees all signatures

## What You Need to Do

### Option 1: Use Demo Database (Quick Start)
The site currently uses placeholder credentials. It won't work until you set up your own Supabase:

### Option 2: Set Up Your Own (5 min - RECOMMENDED)
Follow the instructions in `SUPABASE_SETUP.md`:

```bash
cat SUPABASE_SETUP.md
```

**Summary:**
1. Create free Supabase account
2. Create `signatures` table
3. Copy your API keys
4. Update `index.html` lines ~140-141 with your keys
5. Deploy!

## Where Signatures Appear

On the main page, left sidebar under "TL;DR Summary":
```
┌─────────────────────────┐
│ SIGNATURES (2)          │
├─────────────────────────┤
│ ✓ Casey Glarkin         │
│   casey@sensos.com      │
│   Dec 15, 2025 2:30 PM  │
├─────────────────────────┤
│ ✓ John Smith            │
│   john@manifest.com     │
│   Dec 15, 2025 1:15 PM  │
└─────────────────────────┘
```

## Code Changes Made

1. **Added Supabase client** (`index.html` line 30)
2. **Created tracking functions** (lines 140-180)
   - `saveSignatureToDatabase()` - Saves signatures
   - `fetchAllSignatures()` - Gets all signatures
3. **Created SignatureList component** (lines 3192-3290)
   - Shows all signers
   - Auto-refreshes
   - Pretty UI with icons
4. **Integrated with sign flow** (lines 3356+)
   - Saves to database on sign
   - Shows success/error messages

## Testing

1. Sign the agreement with test data
2. Check Supabase dashboard → Table Editor → `signatures`
3. Refresh the page - signature should appear in the list
4. Sign again with different email - both should show

## Next Steps

⚠️ **IMPORTANT**: Update the Supabase credentials in `index.html` or signatures won't persist!

See `SUPABASE_SETUP.md` for detailed instructions.
