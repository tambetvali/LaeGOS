# LaeGOS Architecture — 2026 Update  
### MongoDB App Services Deprecation & New Backend Model

## 1. Background

MongoDB officially deprecated the majority of **Atlas App Services** features.  
Deprecation notice:  
https://www.mongodb.com/docs/atlas/app-services/deprecation/

As of September 30, 2025, the following App Services components reached **End of Life**:

- Authentication Providers (Google, Email/Password, Custom JWT)
- HTTPS Endpoints
- Functions
- Rules & Permissions
- GraphQL API
- Device Sync
- Static Hosting
- Legacy Data API
- Legacy Triggers

New Atlas projects may not expose App Services UI at all.  
Existing apps continue to run but are frozen and not recommended for new systems.

Because of this, LaeGOS must **not** rely on App Services for authentication, backend logic, or API endpoints.

---

## 2. New Recommended Architecture (MongoDB‑aligned, 2026)

LaeGOS now uses a **three‑layer architecture**:

### Layer 1 — Client (LaeGOS UI)
- Pure frontend (browser or embedded UI)
- Communicates only with the LaeGOS Backend API
- No direct database access
- No App Services SDK

### Layer 2 — LaeGOS Backend (Flask)
The backend is now responsible for:

- OAuth (Google or other providers)
- Session management
- Authorization
- API endpoints (\`/api/...\`)
- Business logic
- Validation
- Rate limiting
- Logging

Flask replaces App Services Functions + HTTPS Endpoints.

### Layer 3 — Database (MongoDB Atlas)
Two supported access methods:

#### Option A — Direct Driver (PyMongo)
Recommended for performance and flexibility.

Docs:  
https://www.mongodb.com/docs/drivers/pymongo/

#### Option B — Atlas Data API (New Model)
HTTP-based CRUD for environments where drivers are not ideal.

Docs:  
https://www.mongodb.com/docs/atlas/api/data-api/

No App Services layer is used.

---

## 3. Authentication Model

### Old Model (Deprecated)
- App Services Google OAuth
- App Services User Identities
- App Services Access Rules

### New Model (2026)
- OAuth handled entirely in Flask
- Use \`authlib\` or Google Identity Services
- Store user sessions in Flask (server-side or JWT)
- Store user profiles in MongoDB manually

This gives LaeGOS full control and avoids deprecated MongoDB features.

---

## 4. API Model

### Old Model (Deprecated)
- App Services HTTPS Endpoints
- App Services Functions

### New Model (2026)
Flask exposes:

\`\`\`
POST /api/login
POST /api/logout
GET  /api/user
GET  /api/data/<collection>
POST /api/data/<collection>
PUT  /api/data/<collection>/<id>
DELETE /api/data/<collection>/<id>
\`\`\`

All logic is implemented in Python.

---

## 5. Data Access Layer

### Option A — PyMongo (recommended)
- Fast
- Full MongoDB feature set
- Ideal for LaeGOS computational modules

### Option B — Atlas Data API
- Pure HTTP
- Good for serverless or restricted environments
- Simpler deployment

---

## 6. Security Model

- No IP whitelisting required if using Data API
- If using PyMongo, configure Network Access for backend server IP
- OAuth tokens validated in Flask
- Backend enforces user permissions
- MongoDB stores only application data

---

## 7. Summary

The LaeGOS backend no longer depends on MongoDB App Services.  
The new architecture is:

**LaeGOS UI → Flask Backend → MongoDB Atlas**

This aligns with MongoDB’s 2026 platform direction and avoids deprecated components.
