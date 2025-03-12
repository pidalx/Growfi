# GROWFI Backend

A FastAPI-based backend for GROWFI, a personal finance management system with AI-powered insights and automated savings features.

## Features

- 🔐 User Authentication with OAuth2 (Google Login)
- 📊 Automated Bank Statement Processing
- 🤖 AI-Powered Budgeting with GPT-4
- 💰 Automated Savings System
- 🧾 SAT Tax Calculation & Explanation for Mexico

## Prerequisites

- Python 3.9+
- PostgreSQL
- AWS RDS or Azure Database for PostgreSQL (for production)
- Google Cloud Project (for OAuth2 and Gmail API)
- OpenAI API Key

## Setup

1. Clone the repository:
```bash
git clone https://github.com/pidalx/growfi-backend.git
cd growfi-backend
```

2. Create and activate a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Copy the example environment file and fill in your values:
```bash
cp .env.example .env
```

5. Set up your database:
- Create a PostgreSQL database
- Update the DATABASE_URL in your .env file

6. Run the application:
```bash
uvicorn app.main:app --reload
```

## API Documentation

Once the server is running, visit:
- Swagger UI: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc

## Environment Variables

Required environment variables:
- `DATABASE_URL`: PostgreSQL connection string
- `SECRET_KEY`: JWT secret key
- `GOOGLE_CLIENT_ID`: Google OAuth2 client ID
- `GOOGLE_CLIENT_SECRET`: Google OAuth2 client secret
- `OPENAI_API_KEY`: OpenAI API key

## Development

To run tests:
```bash
pytest
```

To run linting:
```bash
flake8
```

## Production Deployment

1. Set up AWS RDS or Azure Database for PostgreSQL
2. Update environment variables for production
3. Deploy using Docker or your preferred hosting service
4. Set up proper CORS configuration
5. Enable HTTPS

## License

MIT License
