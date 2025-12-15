# Copilot Instructions for sensos-web-proposal

## Project Overview
This is a v2 web proposal project for Sensos. The codebase is currently in its initial stages.

## Development Setup
- This project runs in a dev container on Ubuntu 24.04.3 LTS
- Available tools: `git`, `gh`, `docker`, `kubectl`, `curl`, `wget`

## Code Structure
*To be populated as the project develops:*
- Source directory structure
- Test directory organization
- Configuration file locations

## Coding Conventions
*To be established as patterns emerge:*
- Naming conventions for components/modules
- File organization patterns
- Import/export patterns

## Development Workflow

### Signature Tracking
- Central database: Supabase (setup guide: `SUPABASE_SETUP.md`)
- Signatures stored in `signatures` table
- Local fallback: `localStorage.getItem('sow_signatures')`
- Auto-refresh every 30 seconds

### Testing Signatures
```javascript
// Check local signatures in browser console:
JSON.parse(localStorage.getItem('sow_signatures') || '[]')

// Manually add test signature:
await saveSignatureToDatabase({
  name: 'Test User',
  email: 'test@example.com',
  title: 'CEO',
  company: 'Test Co',
  signedAt: new Date().toISOString(),
  integrityHash: 'test_hash_123'
})
```

## Testing Practices
*To be defined:*
- Unit test patterns
- Integration test approach
- Test file naming and location

## Architecture Decisions
*Document key architectural choices as they're made:*
- Framework/library selections and rationale
- State management approach
- API integration patterns
- Data flow between components

## Common Tasks
*Add project-specific commands and workflows:*
- How to add new features
- How to debug issues
- How to run locally

---
*Note: This file should be updated as the project grows and patterns emerge. Focus on documenting actual implementation patterns rather than aspirational guidelines.*
