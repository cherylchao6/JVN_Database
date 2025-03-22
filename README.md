# JVN_Database
An intuitive dashboard empowering teams with efficient project management tools for Justice Video Network (JVN) of Ontario Service (Canada).

## Overview
Due to the reliance on Excel for managing various project progress and related data, information was often scattered across different files. Worse still, employees frequently had to update a project’s status across multiple sheets, leading to inconsistencies in data. As a software engineer, I found this situation frustrating, so I decided to design this project. It offers an intuitive and straightforward system for employees to manage data efficiently, helping to streamline collaboration across different teams.

## Quick Demo
https://www.youtube.com/watch?v=BDbANSp7gI0

## System Design
![截圖 2025-03-22 中午12 35 15](https://github.com/user-attachments/assets/d02f5509-5a4b-49f4-9a22-85d6c8399318)



## Database Design
![JVN database design](https://github.com/user-attachments/assets/010ba0f1-eb65-41b5-8cdf-b13e544516ed)

## 🧰 Tech Stack
### Frontend
- **Framework**: Next.js
- **Port**: `3000`
- **Auth**: Microsoft OAuth 2.0 via Azure Active Directory
- **Token Handling**: Receives Microsoft access_token and exchanges it with backend for an API JWT token

### Backend
- **Runtime**: Node.js
- **Port**: `4000` (exposed as `/api`)
- **Auth Flow**:
  1. Validates Microsoft access_token
  2. Issues JWT token for protected API access
- **Database**: PostgreSQL
- **Storage**: Azure Blob Storage (used for file uploads)

### Infrastructure
- **Reverse Proxy**: Nginx
  - Routes `/api/*` to backend
  - Routes all other traffic to frontend
- **Process Manager**: PM2
  - Manages both frontend and backend processes within the VM
- **Deployment Target**: Single Linux-based VM
---

## 🔐 Authentication Flow

1. User logs in via Microsoft Azure AD
2. Frontend receives `access_token` from Azure
3. Frontend sends token to backend API
4. Backend verifies token and responds with custom **JWT**
5. JWT is used for all subsequent authenticated API calls

---

## ☁️ Cloud Services Used

- **Azure Active Directory**: Handles OAuth2.0 authentication
- **Azure Blob Storage**: Stores file assets
- **PostgreSQL**: Stores relational data such as user info, file metadata, etc.

---

## 🖥️ Deployment Overview

All components are deployed and run inside a single Virtual Machine:

```bash
# Start frontend and backend using PM2
pm2 start frontend-app --name frontend
pm2 start backend-app --name backend
