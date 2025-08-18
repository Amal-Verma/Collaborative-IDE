# 🚀 Installation Guide

<div align="center">

![Installation](../assets/installation.svg)

**Complete Setup Guide for Development & Production**

</div>

---

## 🎯 Quick Start

Get Mappa Collaborative IDE running locally in under 5 minutes!

### ⚡ Prerequisites

Ensure you have the following installed:

| Tool | Version | Download |
|------|---------|----------|
| **Node.js** | 18.0+ | [nodejs.org](https://nodejs.org/) |
| **Python** | 3.8+ | [python.org](https://python.org/) |
| **Git** | 2.30+ | [git-scm.com](https://git-scm.com/) |
| **Docker** | 20.0+ (optional) | [docker.com](https://docker.com/) |

### 📦 One-Command Setup

```bash
# Clone and setup everything
curl -fsSL https://raw.githubusercontent.com/Amal-Verma/Collaborative-IDE/main/scripts/quick-setup.sh | bash
```

---

## 🛠️ Manual Installation

### 1️⃣ Clone Repository

```bash
# Clone the repository
git clone https://github.com/Amal-Verma/Collaborative-IDE.git
cd Collaborative-IDE

# Verify directory structure
ls -la
```

### 2️⃣ Backend Setup (FastAPI + Python)

```bash
# Navigate to server directory
cd server

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On macOS/Linux:
source venv/bin/activate
# On Windows:
# venv\Scripts\activate

# Upgrade pip
pip install --upgrade pip

# Install dependencies
pip install -r requirements.txt

# Create environment file
cp .env.example .env

# Edit configuration (see Environment Configuration section)
nano .env
```

### 🔧 Environment Configuration (.env)

```bash
# Database Configuration
SUPABASE_URL=your_supabase_project_url
SUPABASE_KEY=your_supabase_anon_key
SUPABASE_SERVICE_KEY=your_supabase_service_role_key

# JWT Configuration
JWT_SECRET_KEY=your_super_secret_jwt_key_here
JWT_ALGORITHM=HS256
JWT_EXPIRE_MINUTES=15

# Redis Configuration (optional)
REDIS_URL=redis://localhost:6379
REDIS_PASSWORD=your_redis_password

# External Services
GITHUB_CLIENT_ID=your_github_client_id
GITHUB_CLIENT_SECRET=your_github_client_secret

# Liveblocks (for real-time collaboration)
LIVEBLOCKS_SECRET_KEY=your_liveblocks_secret_key

# Stream.io (for video calls)
STREAM_API_KEY=your_stream_api_key
STREAM_API_SECRET=your_stream_api_secret

# Email Service (SendGrid)
SENDGRID_API_KEY=your_sendgrid_api_key
FROM_EMAIL=noreply@yourdomain.com

# Environment
ENVIRONMENT=development
DEBUG=true
LOG_LEVEL=INFO
```

### 🚀 Start Backend Server

```bash
# Development server with auto-reload
uvicorn main:app --reload --host 0.0.0.0 --port 8000

# Production server
uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4
```

**Backend will be available at: `http://localhost:8000`**

### 3️⃣ Frontend Setup (Next.js + React)

Open a new terminal window:

```bash
# Navigate to client directory
cd client

# Install dependencies
npm install
# or with yarn
yarn install

# Create environment file
cp .env.local.example .env.local

# Edit configuration
nano .env.local
```

### 🔧 Frontend Environment Configuration (.env.local)

```bash
# API Configuration
NEXT_PUBLIC_API_URL=http://localhost:8000
NEXT_PUBLIC_WEBSOCKET_URL=ws://localhost:8000

# Supabase Configuration
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key

# Liveblocks Configuration
NEXT_PUBLIC_LIVEBLOCKS_PUBLIC_KEY=your_liveblocks_public_key
LIVEBLOCKS_SECRET_KEY=your_liveblocks_secret_key

# Stream.io Configuration
NEXT_PUBLIC_STREAM_API_KEY=your_stream_api_key

# GitHub OAuth
NEXT_PUBLIC_GITHUB_CLIENT_ID=your_github_client_id

# Analytics (optional)
NEXT_PUBLIC_GOOGLE_ANALYTICS_ID=your_ga_tracking_id

# Environment
NEXT_PUBLIC_ENVIRONMENT=development
NEXT_PUBLIC_DEBUG=true
```

### 🚀 Start Frontend Server

```bash
# Development server
npm run dev
# or with yarn
yarn dev

# Build for production
npm run build
npm start
```

**Frontend will be available at: `http://localhost:3000`**

---

## 🐳 Docker Installation

### 📦 Docker Compose (Recommended)

```bash
# Clone repository
git clone https://github.com/Amal-Verma/Collaborative-IDE.git
cd Collaborative-IDE

# Copy environment files
cp .env.example .env
cp client/.env.local.example client/.env.local

# Edit environment variables
nano .env
nano client/.env.local

# Start all services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

### 🔧 Docker Compose Configuration

```yaml
version: '3.8'

services:
  # Frontend Service
  frontend:
    build:
      context: ./client
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
    environment:
      - NEXT_PUBLIC_API_URL=http://backend:8000
    depends_on:
      - backend
    networks:
      - mappa-network

  # Backend Service
  backend:
    build:
      context: ./server
      dockerfile: Dockerfile
    ports:
      - "8000:8000"
    environment:
      - DATABASE_URL=postgresql://postgres:password@postgres:5432/mappa
      - REDIS_URL=redis://redis:6379
    depends_on:
      - postgres
      - redis
    networks:
      - mappa-network

  # PostgreSQL Database
  postgres:
    image: postgres:15-alpine
    environment:
      - POSTGRES_DB=mappa
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=password
    volumes:
      - postgres_data:/var/lib/postgresql/data
      - ./server/migrations:/docker-entrypoint-initdb.d
    ports:
      - "5432:5432"
    networks:
      - mappa-network

  # Redis Cache
  redis:
    image: redis:7-alpine
    command: redis-server --appendonly yes
    volumes:
      - redis_data:/data
    ports:
      - "6379:6379"
    networks:
      - mappa-network

  # Nginx Reverse Proxy
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf
      - ./nginx/ssl:/etc/nginx/ssl
    depends_on:
      - frontend
      - backend
    networks:
      - mappa-network

volumes:
  postgres_data:
  redis_data:

networks:
  mappa-network:
    driver: bridge
```

---

## 🗄️ Database Setup

### 📊 Supabase Setup (Recommended)

1. **Create Supabase Project**
   ```bash
   # Visit https://supabase.com/dashboard
   # Click "New Project"
   # Choose organization and fill project details
   ```

2. **Get API Keys**
   ```bash
   # Go to Settings > API
   # Copy the following:
   # - Project URL
   # - anon/public key
   # - service_role/secret key
   ```

3. **Run Database Migrations**
   ```bash
   cd server
   python scripts/run_migrations.py
   ```

### 🐘 Local PostgreSQL Setup (Alternative)

```bash
# Install PostgreSQL
# macOS with Homebrew:
brew install postgresql
brew services start postgresql

# Ubuntu/Debian:
sudo apt update
sudo apt install postgresql postgresql-contrib

# Create database
createdb mappa_dev

# Create user
psql -d mappa_dev -c "CREATE USER mappa_user WITH PASSWORD 'secure_password';"
psql -d mappa_dev -c "GRANT ALL PRIVILEGES ON DATABASE mappa_dev TO mappa_user;"

# Run migrations
cd server
python scripts/migrate.py
```

---

## 🔑 External Services Setup

### 🧱 Liveblocks (Real-time Collaboration)

1. **Create Account**: Visit [liveblocks.io](https://liveblocks.io)
2. **Create Project**: Click "New Project" in dashboard
3. **Get API Keys**: Copy Secret Key and Public Key
4. **Add to Environment**: Update `.env` and `.env.local` files

### 📺 Stream.io (Video Calls)

1. **Create Account**: Visit [getstream.io](https://getstream.io)
2. **Create App**: Go to Dashboard > Create App
3. **Get Credentials**: Copy API Key and Secret
4. **Configure**: Update environment files

### 🐙 GitHub OAuth (Code Repository Integration)

1. **GitHub Developer Settings**:
   ```
   Visit: https://github.com/settings/developers
   Click: "New OAuth App"
   ```

2. **App Configuration**:
   ```
   Application name: Mappa Collaborative IDE
   Homepage URL: http://localhost:3000
   Authorization callback URL: http://localhost:3000/auth/github/callback
   ```

3. **Get Credentials**: Copy Client ID and Client Secret

### 📧 SendGrid (Email Service)

1. **Create Account**: Visit [sendgrid.com](https://sendgrid.com)
2. **Generate API Key**:
   ```
   Dashboard > Settings > API Keys > Create API Key
   Select: "Full Access" or customize permissions
   ```
3. **Verify Sender**: Add and verify your sender email

---

## ✅ Verification & Testing

### 🔍 Health Checks

```bash
# Check backend health
curl http://localhost:8000/health

# Expected response:
{
  "status": "healthy",
  "version": "1.0.0",
  "timestamp": "2024-01-20T16:45:00Z",
  "services": {
    "database": "connected",
    "redis": "connected",
    "external_apis": "operational"
  }
}

# Check frontend
curl http://localhost:3000/api/health

# Expected response:
{
  "status": "ok",
  "environment": "development"
}
```

### 🧪 Run Tests

```bash
# Backend tests
cd server
python -m pytest tests/ -v

# Frontend tests
cd client
npm test
# or
yarn test

# E2E tests
npm run test:e2e
```

### 📊 Performance Check

```bash
# Backend performance
cd server
python scripts/benchmark.py

# Frontend performance
cd client
npm run lighthouse
```

---

## 🔧 Development Tools

### 🛠️ Recommended VS Code Extensions

```json
{
  "recommendations": [
    "ms-python.python",
    "bradlc.vscode-tailwindcss",
    "esbenp.prettier-vscode",
    "ms-vscode.vscode-typescript-next",
    "ms-toolsai.jupyter",
    "ms-vscode.vscode-json",
    "redhat.vscode-yaml",
    "ms-vscode-remote.remote-containers"
  ]
}
```

### 🐛 Debugging Configuration

**.vscode/launch.json**:
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: FastAPI",
      "type": "python",
      "request": "launch",
      "program": "${workspaceFolder}/server/main.py",
      "console": "integratedTerminal",
      "env": {
        "ENVIRONMENT": "development"
      }
    },
    {
      "name": "Next.js: debug server-side",
      "type": "node-terminal",
      "request": "launch",
      "command": "npm run dev",
      "cwd": "${workspaceFolder}/client"
    }
  ]
}
```

### 📝 Git Hooks Setup

```bash
# Install pre-commit hooks
cd Collaborative-IDE
pip install pre-commit
pre-commit install

# Test hooks
pre-commit run --all-files
```

---

## 🚨 Troubleshooting

### ❌ Common Issues

#### 1. Port Already in Use
```bash
# Find and kill process using port 8000
lsof -ti:8000 | xargs kill -9

# Find and kill process using port 3000
lsof -ti:3000 | xargs kill -9
```

#### 2. Database Connection Issues
```bash
# Test database connection
cd server
python -c "
from supabase import create_client
import os
from dotenv import load_dotenv

load_dotenv()
url = os.environ['SUPABASE_URL']
key = os.environ['SUPABASE_KEY']

try:
    supabase = create_client(url, key)
    result = supabase.table('users').select('*').limit(1).execute()
    print('Database connection: SUCCESS')
except Exception as e:
    print(f'Database connection: FAILED - {e}')
"
```

#### 3. Missing Dependencies
```bash
# Reinstall backend dependencies
cd server
pip install --upgrade pip
pip install -r requirements.txt --force-reinstall

# Reinstall frontend dependencies
cd client
rm -rf node_modules package-lock.json
npm install
```

#### 4. Environment Variables Not Loading
```bash
# Check environment variables
cd server
python -c "
import os
from dotenv import load_dotenv
load_dotenv()
print('SUPABASE_URL:', os.environ.get('SUPABASE_URL', 'NOT SET'))
print('JWT_SECRET_KEY:', 'SET' if os.environ.get('JWT_SECRET_KEY') else 'NOT SET')
"
```

### 📞 Getting Help

- **GitHub Issues**: [Report bugs](https://github.com/Amal-Verma/Collaborative-IDE/issues)
- **Discussions**: [Community support](https://github.com/Amal-Verma/Collaborative-IDE/discussions)
- **Discord**: [Join our community](https://discord.gg/mappa-ide)
- **Email**: support@mappa-ide.com

### 📚 Additional Resources

- [API Documentation](../api/api-reference.md)
- [Architecture Overview](../architecture/system-architecture.md)
- [Security Guide](../security/security-architecture.md)
- [Contributing Guide](../../CONTRIBUTING.md)

---

<div align="center">

**Next**: [Docker Deployment](docker.md) | **Previous**: [Documentation Home](../README.md)

</div>
