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

## Deployment Guide

### Prerequisites

- Docker installed on your system
- A Replit account for frontend hosting
- Environment variables configured

### Environment Variables

Create a `.env` file with the following variables:

```env
DATABASE_URL=postgresql://user:password@host:port/dbname
JWT_SECRET=your_jwt_secret
OPENAI_API_KEY=your_openai_api_key
```

### Deployment Steps

1. **Build the Docker image:**
   ```bash
   docker build -t growfi-backend .
   ```

2. **Run the container:**
   ```bash
   docker run -d -p 8000:8000 --env-file .env growfi-backend
   ```

3. **Deploy to a cloud provider:**
   - You can deploy to services like Railway, Heroku, or DigitalOcean
   - Make sure to set up the environment variables in your cloud provider's dashboard

### Connecting with Replit Frontend

1. **Update your Replit frontend configuration:**
   - Add your deployed API URL to your frontend's environment variables
   - Example: `VITE_API_URL=https://your-backend-url.com`

2. **Test the connection:**
   - Make sure CORS is properly configured (already done in the backend)
   - Test API endpoints using the frontend's network requests

### API Documentation

Once deployed, you can access the API documentation at:
- Swagger UI: `https://your-backend-url.com/docs`
- ReDoc: `https://your-backend-url.com/redoc`

### Health Check

- Access `https://your-backend-url.com/` to verify the API is running
- You should see a welcome message and status information

### Monitoring

Monitor your application using:
- Application logs via Docker: `docker logs container_id`
- Your cloud provider's monitoring tools
- Database monitoring tools

### Troubleshooting

Common issues and solutions:

1. **CORS Issues:**
   - Verify the frontend URL is properly added to the allowed origins
   - Check browser console for CORS errors

2. **Database Connection:**
   - Ensure DATABASE_URL is correctly set
   - Check database credentials and access

3. **Authentication:**
   - Verify JWT_SECRET is properly set
   - Check token expiration and refresh logic

For more help, please refer to the documentation or open an issue.

## License

MIT License

## Deployment to Railway

### Prerequisites

1. Install Railway CLI:
```bash
# macOS or Linux
brew install railway

# Windows (using scoop)
scoop install railway
```

2. Create a Railway account at https://railway.app/

### Deployment Steps

1. **Login to Railway:**
```bash
railway login
```

2. **Initialize Railway project:**
```bash
railway init
```

3. **Create PostgreSQL Database:**
```bash
railway add postgresql
```

4. **Set up environment variables:**
```bash
# Set required environment variables
railway vars set JWT_SECRET=your_jwt_secret
railway vars set OPENAI_API_KEY=your_openai_api_key
railway vars set GOOGLE_CLIENT_ID=your_google_client_id
railway vars set GOOGLE_CLIENT_SECRET=your_google_client_secret
```

5. **Deploy the application:**
```bash
railway up
```

6. **Get your deployment URL:**
```bash
railway domain
```

### Monitoring and Maintenance

1. **View logs:**
```bash
railway logs
```

2. **Check deployment status:**
```bash
railway status
```

3. **Access Railway dashboard:**
```bash
railway open
```

### Connecting with Replit Frontend

1. **Get your Railway deployment URL:**
```bash
railway domain
```

2. **Update Replit environment variables:**
   - Open your Replit frontend project
   - Go to "Secrets" in the Tools panel
   - Add a new secret:
     - Key: `VITE_API_URL`
     - Value: `https://your-railway-url.railway.app`

3. **Test the connection:**
   - Make a test API call from your frontend
   - Check the Network tab in browser DevTools
   - Verify CORS headers in the response

### Troubleshooting Railway Deployment

1. **Database Connection Issues:**
   - Check Railway PostgreSQL connection string:
     ```bash
     railway vars get DATABASE_URL
     ```
   - Verify database status in Railway dashboard

2. **Application Errors:**
   - Check application logs:
     ```bash
     railway logs
     ```
   - Monitor health check endpoint:
     ```bash
     curl https://your-railway-url.railway.app/health
     ```

3. **Environment Variables:**
   - List all variables:
     ```bash
     railway vars
     ```
   - Verify sensitive variables are set:
     ```bash
     railway vars get JWT_SECRET
     railway vars get OPENAI_API_KEY
     ```

4. **CORS Issues:**
   - Add your Replit domain to allowed origins:
     ```bash
     railway vars set ALLOWED_ORIGINS="https://your-replit-app.repl.co"
     ```
   - Restart the application:
     ```bash
     railway service restart
     ```

### Scaling and Production Tips

1. **Enable Production Mode:**
```bash
railway vars set ENVIRONMENT=production
```

2. **Configure Custom Domain:**
```bash
railway domain custom your-domain.com
```

3. **Set up SSL:**
   - Railway automatically provisions SSL certificates
   - Verify HTTPS is working:
     ```bash
     curl -I https://your-railway-url.railway.app
     ```

4. **Monitor Resource Usage:**
   - Use Railway dashboard metrics
   - Set up alerts for high resource usage

5. **Database Backups:**
   - Enable automatic backups in Railway PostgreSQL settings
   - Schedule regular manual backups:
     ```bash
     railway service backup create
     ```
