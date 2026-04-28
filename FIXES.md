# FIXES.md

## frontend/app.js
- **Line 6**: Hardcoded API URL (`const _URL = "http://localhost:8000";`).
  - **Problem**: This prevents the frontend from communicating with the API when running in containers or different environments.
  - **Fix**: Changed to use `process.env.API_URL || "http://localhost:8000"` so the API URL can be set via environment variable.
