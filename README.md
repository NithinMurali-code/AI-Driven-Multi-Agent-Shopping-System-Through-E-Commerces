# 🛒 AI-Driven Multi-Agent Shopping System Through E-Commerce

![Node.js](https://img.shields.io/badge/Node.js-backend-green)
![Express](https://img.shields.io/badge/Express.js-API-lightgrey)
![React](https://img.shields.io/badge/React-frontend-blue)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-database-blue)
![Drizzle](https://img.shields.io/badge/Drizzle-ORM-yellow)

A full-stack e-commerce platform where **autonomous agents** handle product search, cart management and order management. Orders are processed in real time against live inventory, with data integrity checks that prevent race conditions and unauthorized order manipulation. Access is secured with **JWT authentication** and **role-based access control (RBAC)**.

<!-- EDIT: add your live demo link here, e.g. **Live demo:** https://your-app.up.railway.app -->

---

## ✨ Features

| | |
|---|---|
| 🤖 **Multi-agent design** | Separate autonomous agents for search, cart and order management |
| 📦 **Inventory-aware orders** | Order processing checks stock in real time before confirming |
| 🛡️ **Data integrity checks** | Guards against race conditions (for example two buyers taking the last item) and unauthorized order changes |
| 🔐 **Secure access** | JWT authentication with role-based access control (RBAC) |
| 🗄️ **Reliable data layer** | PostgreSQL accessed through the Drizzle ORM |
| 🖥️ **Modern frontend** | React user interface |
| ☁️ **Deployed** | Hosted on Railway |

---

## 🧭 How it works

```
 React frontend
       │
       ▼
 Express API  ──►  Auth middleware (JWT + RBAC)
       │
       ▼
 ┌───────────┬───────────┬────────────────┐
 │  Search   │   Cart    │     Order      │   ← autonomous agents
 │   agent   │   agent   │     agent      │
 └─────┬─────┴─────┬─────┴────────┬───────┘
       └───────────┴──────────────┘
                   │
                   ▼
        PostgreSQL (via Drizzle ORM)
        products · carts · orders · inventory
```

1. A user signs in and receives a JWT; every protected request is checked for a valid token and the right role.
2. The **search agent** finds matching products.
3. The **cart agent** manages what the user has chosen.
4. The **order agent** checks live inventory and places the order, using integrity checks so stock is never oversold and orders cannot be tampered with.

---

## 🛠️ Tech stack

| Layer | Technology |
|---|---|
| Frontend | React |
| Backend | Node.js, Express.js |
| Database | PostgreSQL with Drizzle ORM |
| Authentication | JWT, role-based access control (RBAC) |
| Deployment | Railway |

---

## 🏗️ 1. Technical Architecture Overview

Before you start, here is a quick look at the system structure:

- **Frontend**: A performance-optimized React application (Vite + Tailwind CSS).
- **Backend API**: A Node.js (Express) server handling product catalogs, user authentication, and AI logic.
- **Database**: PostgreSQL with Drizzle ORM for high-integrity data storage.
- **AI Integrations**: Native support for OpenAI GPT-4o and local LLMs via Ollama.

---

## 🛠️ 2. Software Prerequisites

Ensure the following software is installed on your computer:

1.  **Node.js (v18.0.0 or higher)**: [Download here](https://nodejs.org/)
2.  **PostgreSQL (v14 or higher)**: [Download here](https://www.postgresql.org/download/)
    - *Default user:* `postgres`
    - *Default password:* `postgres` (or your chosen password)
3.  **Git**: [Download here](https://git-scm.com/downloads) (Optional, for cloning)

---

## 🚀 3. One-Click Setup (Recommended)

We have provided an automated script to handle the heavy lifting.

1.  Open the project folder in your file explorer.
2.  Double-click **`setup_project.bat`**.
3.  Follow the prompts in the terminal window:
    - It will check for Node.js and installed dependencies.
    - It will install **pnpm** (if missing).
    - It will create a default `.env` file.
    - **Select 'y'** when asked to initialize the database (ensure PostgreSQL is running first).

---

## ⚙️ 4. Manual Configuration (Advanced)

If you prefer to set up manually, follow these steps:

### A. Environment Variables
Create a `.env` file in the root directory:
```env
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/ecommerce
JWT_SECRET=your_secret_here
AI_INTEGRATIONS_OPENAI_API_KEY=your_key_here
AI_INTEGRATIONS_OPENAI_MODEL=gpt-4o
```

### B. Installation
Run the following in your terminal:
```bash
# Install pnpm (if not already installed)
npm install -g pnpm

# Install project dependencies
pnpm install
```

### C. Database Initialization
```bash
# Create tables
pnpm db:push

# Seed initial product data
pnpm db:seed
```

---

## 🏃 5. Launching the Platform

To start the servers and the store:

1.  Double-click **`run_project.bat`**.
2.  Wait for the terminal windows to initialize (approx. 5-10 seconds).
3.  The store will automatically open in your browser at: 
    👉 **http://localhost:5173**

---

## 🔐 6. Admin Panel & Management

- **Admin URL**: Navigate to `/admin/products` in the store.
- **Privileges**: Any account registered with an email containing the word `"admin"` (e.g., `admin@test.com`) will automatically receive full administrative access to manage products and stock.

---

## 🤖 7. AI Features (Optional)

### Using Ollama (Local AI)
If you want to run AI features locally without an OpenAI API key:
1.  Install [Ollama](https://ollama.com/).
2.  Pull a model: `ollama pull llama3`.
3.  Ensure Ollama is running.
4.  The application will automatically attempt to use the local endpoint if configured.

---

## ⚠️ 8. Troubleshooting

- **Database Connection Refused**: Ensure PostgreSQL is running. Check your password in `.env`.
- **Port Already in Use**: Close any applications running on ports `5173` (Frontend) or `5000` (Backend).
- **Missing Images**: Ensure you have an active internet connection as the product images are served via Unsplash.

---


## 🚀 Getting started

**Requirements:** Node.js (LTS version) and a running PostgreSQL database.

```bash
git clone https://github.com/NithinMurali-code/AI-Driven-Multi-Agent-Shopping-System-Through-E-Commerces.git
cd AI-Driven-Multi-Agent-Shopping-System-Through-E-Commerces
npm install
```
<!-- EDIT: if your client and server are in separate folders, run npm install in each, e.g. cd server && npm install, then cd ../client && npm install -->

Create a `.env` file in the project root (never commit it):

```env
DATABASE_URL=postgresql://USER:PASSWORD@localhost:5432/DB_NAME
JWT_SECRET=your_long_random_secret
PORT=5000
```
<!-- EDIT: replace the variable names above with the ones your project actually reads -->

Set up the database tables and start the app:

```bash
npx drizzle-kit push
npm run dev
```
<!-- EDIT: confirm these against the "scripts" section of your package.json -->

---

## 🔒 Security notes

- Secrets such as the database URL and JWT secret live in `.env`, which is excluded from Git.
- Protected routes require a valid JWT, and RBAC limits what each role can do.
- Order handling includes integrity checks to prevent race conditions and unauthorized manipulation.

---

## 📸 Screenshots

<img width="625" height="372" alt="image" src="https://github.com/user-attachments/assets/782848f1-4ec3-499a-9782-cfdc8919b46b" />

<img width="692" height="423" alt="image" src="https://github.com/user-attachments/assets/70eccabb-000e-4ac5-9a3e-12cce65f72d4" />

<img width="730" height="412" alt="image" src="https://github.com/user-attachments/assets/e5de33c1-33ce-4a00-a1d5-c23ad54d6c22" />

<img width="566" height="405" alt="image" src="https://github.com/user-attachments/assets/7e789758-dd74-4ce0-85a8-a0c5abf74197" />

<img width="545" height="414" alt="image" src="https://github.com/user-attachments/assets/d0f84962-03c2-4dac-8f4e-07898d77d19e" />


---

## 🔮 Future scope

Payment gateway integration · product recommendations · order tracking and notifications · automated tests and CI.

---

## 👤 Author

** Vemula Nithin Murali ** - B.Tech CSE, Holy Mary Institute of Technology and Science
GitHub: [NithinMurali-code](https://github.com/NithinMurali-code)
