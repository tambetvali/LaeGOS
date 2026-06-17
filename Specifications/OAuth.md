# 🧩 LaeGOS Authentication & Boot Architecture  
### _MongoDB Atlas App Services Integration Plan_

---

## 🚀 Overview

This document defines the **authentication and boot architecture** for LaeGOS, using **MongoDB Atlas App Services OAuth** as the *only* login/logout mechanism.

The system behaves like a **stateless Linux live CD**, where the OS boots in memory and optionally binds to a cloud user account.

---

## 🖥️ Main Screen Responsibilities

The main screen is the **entry point** and exposes exactly **two buttons**:

### ✔ **Start Up**
- Boots the stateless OS  
- If a MongoDB user is authenticated → OS boots in **user mode**  
- If not → OS boots in **anonymous mode**

### ✔ **User Authentication**
- Opens the dedicated `/login` page  
- `/login` triggers **MongoDB OAuth login**  
- After login, user is redirected back to the main screen  
- The main screen does **not** implement login logic  
- Login/logout is a **side-effect** of MongoDB App Services

---

## 🔐 Authentication Model

### ✔ Single authentication authority  
MongoDB Atlas App Services is the **only** login/logout system.

### ✔ Main screen does not handle credentials  
It only triggers the OAuth flow.

### ✔ Login page is not a UI  
It is a **redirect trigger** for OAuth.

### ✔ Logout is also MongoDB‑driven  
The main screen simply calls `user.logOut()`.

---

## 🔄 OS Boot Behavior

### When user is authenticated:
- OS boots with:
  - User partition  
  - User database  
  - User-specific state  

### When user is not authenticated:
- OS boots in **anonymous stateless mode**

### While OS is running:
- ❌ User cannot switch accounts  
- ❌ User cannot log in or out  
- ✔ Only option: **Restart OS**

### Restarting OS:
- Returns to main screen  
- User may:
  - Authenticate with MongoDB  
  - Or run anonymously again  

---

## 🧠 State Model Summary

| State | Description |
|------|-------------|
| **Main Screen (No User)** | Shows Start Up + User Authentication |
| **Main Screen (User Authenticated)** | Shows Start Up + “Logged in as …” |
| **OS Running** | No login/logout allowed; restart required |
| **Restart** | Returns to main screen |

---

## 🛠️ Implementation Snippets

### Main Screen Logic  
\`\`\`js
import { app } from "./realm";

export default function MainScreen() {
  const user = app.currentUser;

  return (
    <div>
      <button onClick={() => startOS(user)}>
        Start Up
      </button>

      {!user && (
        <button onClick={() => window.location.href = "/login"}>
          User Authentication
        </button>
      )}

      {user && (
        <div>Logged in as {user.profile.email}</div>
      )}
    </div>
  );
}
\`\`\`

---

### Login Page (OAuth Redirect Trigger)  
\`\`\`js
import { app } from "./realm";

export default function LoginPage() {
  async function startOAuth() {
    const credentials = Realm.Credentials.google(); // or github, apple, etc.
    await app.logIn(credentials);
    window.location.href = "/";
  }

  startOAuth();

  return <div>Redirecting…</div>;
}
\`\`\`

---

### OS Boot Logic  
\`\`\`js
function startOS(user) {
  if (user) {
    launchOS({ partition: user.id });
  } else {
    launchOS({ partition: "anonymous" });
  }
}
\`\`\`

---

## 📦 MongoDB Partitioning Strategy

Each authenticated user receives:

- Their own database partition  
- Their own isolated data  
- Their own OS state  

Anonymous users share:

- A stateless, ephemeral partition  
- No persistence  

---

## 🧭 Summary

- ✔ Main screen is the **only** place where user switching begins  
- ✔ Login/logout is **not** implemented by the main screen  
- ✔ MongoDB OAuth is the **sole** authentication mechanism  
- ✔ OS cannot switch users while running  
- ✔ Restart is required to change user  
- ✔ Architecture mirrors a **stateless Linux live CD** with optional cloud identity  

---

## 📘 Status

- [x] Architecture defined  
- [ ] Implement OAuth providers  
- [ ] Implement partition rules  
- [ ] Integrate into LaeGOS-Widgets  

---
