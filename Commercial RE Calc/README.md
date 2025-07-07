# Commercial RE Calculator

AI-Enhanced Deal Analyzer for Multifamily & Commercial Real Estate Investments

## 🏗️ Project Overview

This is a SaaS-ready, AI-enhanced deal analyzer that automatically computes key financial metrics, generates red-flag alerts, and summarizes investment insights using GPT-level intelligence for commercial real estate investments.

### Key Features

- **Multi-step Deal Input**: Property details, rent roll upload, expenses & financing, exit strategy
- **File Upload Support**: CSV/Excel rent rolls and PDF T12s
- **AI-Enhanced Analysis**: Investment summaries and red flag detection
- **Financial Calculations**: NOI, Cap Rate, IRR, Equity Multiple, DSCR, and more
- **Interactive Visualizations**: Cash flow curves, IRR waterfall, sensitivity tables
- **PDF Export**: Professionally formatted investment reports
- **Multi-tenant Architecture**: Ready for SaaS deployment

## 🛠️ Tech Stack

### Frontend
- **Framework**: Next.js 14 (App Router)
- **UI Library**: Chakra UI
- **File Upload**: react-dropzone, xlsx, pdfjs-dist
- **Charts**: Plotly.js, Recharts
- **Forms**: react-hook-form with Zod validation
- **Authentication**: Auth0
- **Payments**: Stripe

### Backend
- **Framework**: FastAPI (Python)
- **AI Integration**: OpenAI API
- **File Parsing**: pandas, openpyxl, tabula-py, pdfplumber
- **PDF Export**: WeasyPrint
- **Database**: PostgreSQL with SQLAlchemy
- **Multi-tenant**: Row-Level Security (RLS)

### Hosting
- **Frontend**: Vercel
- **Backend**: Render/Railway/AWS
- **Database**: Supabase or AWS RDS

## 📦 Installation & Setup

### Prerequisites

1. **Node.js** (v18 or higher)
   ```bash
   # Download from https://nodejs.org/
   # Or use nvm (Node Version Manager)
   nvm install 18
   nvm use 18
   ```

2. **Python** (v3.9 or higher)
   ```bash
   # Download from https://python.org/
   # Or use pyenv
   pyenv install 3.9.0
   pyenv global 3.9.0
   ```

3. **PostgreSQL** (v13 or higher)
   ```bash
   # Download from https://postgresql.org/
   # Or use Docker
   docker run --name postgres -e POSTGRES_PASSWORD=password -p 5432:5432 -d postgres:13
   ```

### Frontend Setup

1. **Navigate to frontend directory**
   ```bash
   cd frontend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   ```bash
   # Create .env.local file
   cp .env.example .env.local
   ```

   Add the following to `.env.local`:
   ```env
   NEXT_PUBLIC_API_URL=http://localhost:8000
   NEXT_PUBLIC_AUTH0_DOMAIN=your-auth0-domain
   NEXT_PUBLIC_AUTH0_CLIENT_ID=your-auth0-client-id
   NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=your-stripe-publishable-key
   ```

4. **Start development server**
   ```bash
   npm run dev
   ```

   The frontend will be available at `http://localhost:3000`

### Backend Setup

1. **Navigate to backend directory**
   ```bash
   cd backend
   ```

2. **Create virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables**
   ```bash
   # Create .env file
   cp .env.example .env
   ```

   Add the following to `.env`:
   ```env
   DATABASE_URL=postgresql://username:password@localhost:5432/commercial_re_calc
   OPENAI_API_KEY=your-openai-api-key
   AUTH0_DOMAIN=your-auth0-domain
   AUTH0_AUDIENCE=your-auth0-audience
   STRIPE_SECRET_KEY=your-stripe-secret-key
   STRIPE_WEBHOOK_SECRET=your-stripe-webhook-secret
   ```

5. **Run database migrations**
   ```bash
   alembic upgrade head
   ```

6. **Start development server**
   ```bash
   uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
   ```

   The backend API will be available at `http://localhost:8000`

## 🚀 Development

### Project Structure

```
├── frontend/                 # Next.js frontend
│   ├── src/
│   │   ├── app/             # App Router pages
│   │   │   ├── steps/       # Form step components
│   │   │   └── ...
│   │   ├── types/           # TypeScript types
│   │   └── utils/           # Utility functions
│   ├── package.json
│   └── ...
├── backend/                  # FastAPI backend
│   ├── app/
│   │   ├── api/             # API routes
│   │   ├── models/          # Database models
│   │   ├── services/        # Business logic
│   │   └── utils/           # Utility functions
│   ├── requirements.txt
│   └── ...
└── README.md
```

### Key Components

#### Frontend Components

1. **DealAnalyzer** (`src/components/DealAnalyzer.tsx`)
   - Main orchestrator component
   - Handles multi-step form flow
   - Manages state and API calls

2. **Form Steps** (`src/components/steps/`)
   - `PropertyDetailsStep.tsx` - Basic property info
   - `RentRollStep.tsx` - Rent roll data & file upload
   - `ExpensesFinancingStep.tsx` - Operating expenses & loan terms
   - `ExitStrategyStep.tsx` - Exit assumptions & market data

3. **DealResults** (`src/components/DealResults.tsx`)
   - Displays analysis results
   - Shows AI insights and red flags
   - Placeholder for charts and visualizations

#### Backend Services

1. **Financial Calculations** (`app/services/calculations.py`)
   - NOI, Cap Rate, IRR, Equity Multiple calculations
   - Cash flow projections
   - Sensitivity analysis

2. **File Parsing** (`app/services/file_parser.py`)
   - CSV/Excel rent roll parsing
   - PDF T12 extraction
   - Data validation and cleaning

3. **AI Analysis** (`app/services/ai_analysis.py`)
   - OpenAI API integration
   - Investment summary generation
   - Red flag detection

### Development Workflow

1. **Start both servers**
   ```bash
   # Terminal 1 - Frontend
   cd frontend && npm run dev

   # Terminal 2 - Backend
   cd backend && uvicorn app.main:app --reload
   ```

2. **Database changes**
   ```bash
   # Create new migration
   alembic revision --autogenerate -m "description"

   # Apply migrations
   alembic upgrade head
   ```

3. **Testing**
   ```bash
   # Frontend tests
   cd frontend && npm test

   # Backend tests
   cd backend && pytest
   ```

## 🔧 Configuration

### Environment Variables

#### Frontend (.env.local)
- `NEXT_PUBLIC_API_URL` - Backend API URL
- `NEXT_PUBLIC_AUTH0_DOMAIN` - Auth0 domain
- `NEXT_PUBLIC_AUTH0_CLIENT_ID` - Auth0 client ID
- `NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY` - Stripe publishable key

#### Backend (.env)
- `DATABASE_URL` - PostgreSQL connection string
- `OPENAI_API_KEY` - OpenAI API key
- `AUTH0_DOMAIN` - Auth0 domain
- `AUTH0_AUDIENCE` - Auth0 API audience
- `STRIPE_SECRET_KEY` - Stripe secret key
- `STRIPE_WEBHOOK_SECRET` - Stripe webhook secret

### Database Setup

1. **Create database**
   ```sql
   CREATE DATABASE commercial_re_calc;
   ```

2. **Run migrations**
   ```bash
   alembic upgrade head
   ```

3. **Seed data (optional)**
   ```bash
   python -m app.scripts.seed_data
   ```

## 🚀 Deployment

### Frontend (Vercel)

1. **Connect repository to Vercel**
2. **Set environment variables in Vercel dashboard**
3. **Deploy automatically on push to main branch**

### Backend (Render/Railway)

1. **Connect repository to Render/Railway**
2. **Set environment variables**
3. **Configure build command**: `pip install -r requirements.txt`
4. **Configure start command**: `uvicorn app.main:app --host 0.0.0.0 --port $PORT`

### Database (Supabase)

1. **Create Supabase project**
2. **Get connection string from Settings > Database**
3. **Update DATABASE_URL in backend environment**

## 📊 Features Roadmap

### MVP (Current)
- ✅ Multi-step deal input form
- ✅ Basic financial calculations
- ✅ AI analysis integration
- ✅ Results display
- ✅ PDF export (placeholder)

### Phase 2
- 🔄 Interactive charts and visualizations
- 🔄 Advanced file parsing (PDF T12s)
- 🔄 Sensitivity analysis tables
- 🔄 Deal comparison tools

### Phase 3
- 📋 Authentication and user management
- 📋 Deal saving and sharing
- 📋 Subscription management
- 📋 Advanced AI features

### Phase 4
- 📋 Market data integration
- 📋 Collaboration features
- 📋 Mobile app
- 📋 API for third-party integrations

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes
4. Add tests if applicable
5. Commit your changes: `git commit -m 'Add feature'`
6. Push to the branch: `git push origin feature-name`
7. Submit a pull request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

For support and questions:
- Create an issue in the GitHub repository
- Email: support@commercialrecalc.com
- Documentation: [docs.commercialrecalc.com](https://docs.commercialrecalc.com)

## 🔗 Links

- [Live Demo](https://commercialrecalc.com)
- [API Documentation](https://api.commercialrecalc.com/docs)
- [User Guide](https://docs.commercialrecalc.com/guide)
- [Developer Documentation](https://docs.commercialrecalc.com/dev) 