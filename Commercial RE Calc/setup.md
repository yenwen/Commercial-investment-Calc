# Commercial RE Calculator - Setup Guide

## 🚀 Quick Start

This guide will help you set up the Commercial RE Calculator project on your local machine.

## Prerequisites

Before you begin, make sure you have the following installed:

### 1. Node.js (v18 or higher)
```bash
# Check if Node.js is installed
node --version

# If not installed, download from https://nodejs.org/
# Or use nvm (Node Version Manager):
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
nvm install 18
nvm use 18
```

### 2. Python (v3.9 or higher)
```bash
# Check if Python is installed
python --version

# If not installed, download from https://python.org/
# Or use pyenv:
curl https://pyenv.run | bash
pyenv install 3.9.0
pyenv global 3.9.0
```

### 3. PostgreSQL (v13 or higher)
```bash
# Option 1: Install PostgreSQL locally
# Download from https://postgresql.org/

# Option 2: Use Docker
docker run --name postgres -e POSTGRES_PASSWORD=password -p 5432:5432 -d postgres:13
```

## Frontend Setup

### 1. Install Node.js Dependencies
```bash
cd frontend
npm install
```

### 2. Create Environment File
```bash
# Create .env.local file
cp .env.example .env.local
```

Edit `.env.local` and add your configuration:
```env
NEXT_PUBLIC_API_URL=http://localhost:8000
NEXT_PUBLIC_AUTH0_DOMAIN=your-auth0-domain
NEXT_PUBLIC_AUTH0_CLIENT_ID=your-auth0-client-id
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=your-stripe-publishable-key
```

### 3. Start Development Server
```bash
npm run dev
```

The frontend will be available at `http://localhost:3000`

## Backend Setup

### 1. Create Python Virtual Environment
```bash
cd backend
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 2. Install Python Dependencies
```bash
pip install -r requirements.txt
```

### 3. Create Environment File
```bash
# Create .env file
cp .env.example .env
```

Edit `.env` and add your configuration:
```env
DATABASE_URL=postgresql://username:password@localhost:5432/commercial_re_calc
OPENAI_API_KEY=your-openai-api-key
AUTH0_DOMAIN=your-auth0-domain
AUTH0_AUDIENCE=your-auth0-audience
STRIPE_SECRET_KEY=your-stripe-secret-key
STRIPE_WEBHOOK_SECRET=your-stripe-webhook-secret
```

### 4. Set Up Database
```bash
# Create database (if using local PostgreSQL)
createdb commercial_re_calc

# Run migrations
alembic upgrade head
```

### 5. Start Development Server
```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

The backend API will be available at `http://localhost:8000`

## Third-Party Services Setup

### 1. Auth0 Setup
1. Create an Auth0 account at https://auth0.com
2. Create a new application (Single Page Application)
3. Configure callback URLs: `http://localhost:3000/callback`
4. Get your domain and client ID
5. Add them to your environment files

### 2. OpenAI Setup
1. Create an OpenAI account at https://openai.com
2. Generate an API key
3. Add it to your backend `.env` file

### 3. Stripe Setup (Optional for MVP)
1. Create a Stripe account at https://stripe.com
2. Get your publishable and secret keys
3. Add them to your environment files

## Development Workflow

### 1. Start Both Servers
```bash
# Terminal 1 - Frontend
cd frontend && npm run dev

# Terminal 2 - Backend
cd backend && uvicorn app.main:app --reload
```

### 2. Access the Application
- Frontend: http://localhost:3000
- Backend API: http://localhost:8000
- API Documentation: http://localhost:8000/docs

### 3. Database Management
```bash
# Create new migration
alembic revision --autogenerate -m "description"

# Apply migrations
alembic upgrade head

# Rollback migration
alembic downgrade -1
```

## Troubleshooting

### Common Issues

1. **Node.js not found**
   - Install Node.js from https://nodejs.org/
   - Or use nvm: `nvm install 18 && nvm use 18`

2. **Python not found**
   - Install Python from https://python.org/
   - Or use pyenv: `pyenv install 3.9.0 && pyenv global 3.9.0`

3. **PostgreSQL connection failed**
   - Check if PostgreSQL is running
   - Verify connection string in `.env`
   - Create database: `createdb commercial_re_calc`

4. **Port already in use**
   - Kill process using the port: `lsof -ti:3000 | xargs kill -9`
   - Or use different ports in your environment files

5. **Module not found errors**
   - Make sure you're in the correct directory
   - Install dependencies: `npm install` (frontend) or `pip install -r requirements.txt` (backend)
   - Check if virtual environment is activated (backend)

### Getting Help

- Check the [README.md](README.md) for detailed documentation
- Review the API documentation at http://localhost:8000/docs
- Create an issue in the GitHub repository

## Next Steps

Once you have the basic setup running:

1. **Explore the Application**
   - Navigate through the multi-step form
   - Test file uploads
   - Review the analysis results

2. **Customize the Application**
   - Modify the UI components in `frontend/src/components/`
   - Add new API endpoints in `backend/app/api/routes/`
   - Update financial calculations in `backend/app/services/`

3. **Add Features**
   - Implement authentication
   - Add more chart visualizations
   - Enhance AI analysis capabilities

4. **Deploy to Production**
   - Frontend: Deploy to Vercel
   - Backend: Deploy to Render/Railway/AWS
   - Database: Use Supabase or AWS RDS

## Environment Variables Reference

### Frontend (.env.local)
| Variable | Description | Example |
|----------|-------------|---------|
| `NEXT_PUBLIC_API_URL` | Backend API URL | `http://localhost:8000` |
| `NEXT_PUBLIC_AUTH0_DOMAIN` | Auth0 domain | `your-app.auth0.com` |
| `NEXT_PUBLIC_AUTH0_CLIENT_ID` | Auth0 client ID | `your-client-id` |
| `NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY` | Stripe publishable key | `pk_test_...` |

### Backend (.env)
| Variable | Description | Example |
|----------|-------------|---------|
| `DATABASE_URL` | PostgreSQL connection string | `postgresql://user:pass@localhost/db` |
| `OPENAI_API_KEY` | OpenAI API key | `sk-...` |
| `AUTH0_DOMAIN` | Auth0 domain | `your-app.auth0.com` |
| `AUTH0_AUDIENCE` | Auth0 API audience | `https://your-api.com` |
| `STRIPE_SECRET_KEY` | Stripe secret key | `sk_test_...` |
| `STRIPE_WEBHOOK_SECRET` | Stripe webhook secret | `whsec_...` | 