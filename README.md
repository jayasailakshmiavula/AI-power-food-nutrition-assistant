# Campus AI Hub — AI Nutrition Assistant & Smart Lost and Found Portal

A production-ready, full-stack campus web application uniting two essential university utilities into one unified experience:
1. **AI Nutrition Assistant**: Personalized student meal planning based on hostel budgets, fitness goals, and mess ingredients, coupled with an AI food analyzer and categorized grocery list sync.
2. **Campus Lost & Found Portal**: Intelligent property recovery portal featuring automated multi-factor AI correlation, transparent match scores, tracking IDs, and ownership claim verification workflows.

---

## 🌟 Key Features

### 🥗 1. AI Nutrition Assistant
- **Student Onboarding**: Collects age, gender, height, weight, activity level, primary fitness goal, diet type (Vegetarian, Vegan, High Protein, etc.), budget, and strict allergy exclusions.
- **AI Meal Planner**: Generates complete 4-meal daily schedules (Breakfast, Lunch, Snack, Dinner) detailing calories, macronutrients, prep instructions, and estimated costs in ₹.
- **AI Food & Image Analyzer**: Analyze campus meals from text or uploaded photos to get instant nutritional scoring (0–100) and healthier swaps.
- **Daily Nutrition Summary & Meal Tracker**: Interactive calorie and macronutrient progress with Recharts weekly trends and weight tracking.
- **Automated Grocery Checklist**: Converts planned meals into categorized grocery lists (Vegetables, Fruits, Grains, Protein, Dairy, Spices, Other).

### 🔍 2. Campus Lost & Found Portal
- **Directory & Live Filtering**: Search lost and found belongings by keyword, location, date, category, and status.
- **Report Lost Item**: Generates formal university tracking IDs (e.g. `LF-2026-000123`) and instantly triggers background AI correlation against found items.
- **Report Found Item**: Quick logging for items deposited at campus security desks, library counters, or tech labs.
- **AI Item Matching Engine**: Computes similarity scores (0–100%) and explains reasons (matching category, brand, physical identifiers, campus zone, date range).
- **Ownership Verification & Claim System**: Allows students to submit unique identifying details before admin approval.

### 🛡️ 3. Administrative Portal & RBAC
- **Analytics Dashboard**: Tracks recovery rates, monthly trends, property distribution across campus buildings, and nutrition module adoption.
- **Claims Verification**: Review student claims, request additional proof, approve or decline requests.
- **Role-Based Access Control**: Student vs. Campus Admin roles with pre-configured demo personas.

---

## 🛠️ Technology Stack

- **Frontend**: React 19, TypeScript, Tailwind CSS, Recharts, Lucide React, Vite.
- **Backend**: Node.js, Express.js, TypeScript (`tsx`), JWT authentication, bcryptjs password hashing.
- **Database Architecture**: Prisma ORM schema (`prisma/schema.prisma`) and persistent storage engine (`server/src/db/dbStore.ts`).
- **AI Integration**: Google Gen AI SDK (`@google/genai`) with configurable `AI_API_KEY` or `GEMINI_API_KEY` and built-in procedural heuristic fallback for demo environments.

---

## 🔑 Demo Credentials

For demonstration and testing, you can use the 1-click persona switcher in the header or sign in with:

| Role | Email | Password | Details |
| :--- | :--- | :--- | :--- |
| **Student** | `student@campus.edu` | `Password123!` | Aarav Sharma (Computer Science, 3rd Year) |
| **Admin** | `admin@campus.edu` | `AdminPassword123!` | Prof. Elena Vance (Campus Security & Operations) |

---

## ⚙️ Environment Variables

Configure your `.env` file using `.env.example`:

```env
# Database URL
DATABASE_URL="postgresql://user:password@localhost:5432/campus_ai_hub?schema=public"

# Authentication
JWT_SECRET="campus-ai-hub-super-secret-jwt-key-2026"

# AI Service Configuration
AI_API_KEY=""
AI_MODEL="gemini-3.8-flash"
GEMINI_API_KEY=""

# Server
PORT=3000
CLIENT_URL="http://localhost:3000"
```

*Note: If no AI API key is configured, the system automatically uses the intelligent local heuristic and procedural generator.*

---

## 🚀 Running the Project

```bash
# 1. Install dependencies
npm install

# 2. Run the fullstack development server
npm run dev

# 3. Production build
npm run build
npm run start
```

---

## 📡 REST API Documentation

### Authentication
- `POST /api/auth/register` - Create student/admin account
- `POST /api/auth/login` - Authenticate and return JWT
- `GET /api/auth/me` - Fetch profile of logged-in user

### Nutrition
- `GET /api/nutrition/profile` - Get user nutrition constraints
- `PUT /api/nutrition/profile` - Update targets, budget, and allergies
- `POST /api/nutrition/meal-plan/generate` - Generate personalized AI meal plan
- `GET /api/nutrition/meal-plans` - List saved meal plans
- `POST /api/nutrition/analyze-food` - AI nutritional scoring and alternatives
- `GET /api/nutrition/daily-summary` - Daily calories, macros, and weekly charts
- `GET /api/nutrition/grocery-list` - Get categorized grocery checklist

### Lost & Found
- `GET /api/lost-found` - Search and filter campus items
- `POST /api/lost-found/lost` - Report lost item & generate tracking ID
- `POST /api/lost-found/found` - Report found item deposited on campus
- `POST /api/lost-found/:id/claim` - Submit verification claim on found item
- `GET /api/lost-found/all-matches` - Get AI correlation matches

### Administration
- `GET /api/admin/dashboard` - Campus statistics and Recharts analytics
- `GET /api/admin/claims` - Review pending ownership claims
- `PUT /api/admin/claims/:id` - Approve or reject claim
- `PUT /api/admin/items/:id/status` - Update item recovery lifecycle status
