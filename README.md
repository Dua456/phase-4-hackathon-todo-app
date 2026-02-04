# Todo Application with AI Assistant and OAuth Integration

A modern, feature-rich todo application built with Next.js, FastAPI, and PostgreSQL, featuring AI-powered task management, Google OAuth authentication, and real-time task collaboration.

## Features

### 📝 Task Management
- Create, read, update, and delete tasks
- Set task priorities (Low, Medium, High)
- Add tags for better organization
- Mark tasks as complete/incomplete
- Filter and search tasks

### 🔐 Authentication
- Google OAuth integration
- GitHub OAuth integration
- Traditional email/password authentication
- Secure JWT-based authentication
- OAuth callback handling with proper redirects

### 🤖 AI Assistant
- AI-powered task creation and management
- Natural language processing for task commands
- Real-time chat interface for task assistance
- Smart task suggestions

### 🎨 User Experience
- Dark/light theme support
- Responsive design for all devices
- Modern UI with gradient backgrounds
- Intuitive dashboard with statistics cards
- User profile management

### 🛡️ Security
- JWT token-based authentication
- Secure password hashing with bcrypt
- CORS configuration for safe cross-origin requests
- OAuth2 protocol compliance

## Tech Stack

### Frontend
- **Next.js 14** - React framework with App Router
- **TypeScript** - Type-safe JavaScript
- **Tailwind CSS** - Utility-first CSS framework
- **React Icons** - SVG icons for React projects

### Backend
- **FastAPI** - Modern Python web framework
- **SQLModel** - SQL database modeling
- **PostgreSQL** - Object-relational database
- **Pydantic** - Data validation library

### Authentication & Security
- **OAuth 2.0** - Industry-standard protocol
- **JWT** - JSON Web Tokens for secure authentication
- **Passlib** - Password hashing library
- **python-jose** - JWT encoding/decoding

### AI Integration
- **Groq API** - AI inference engine
- **Langchain** - Framework for AI applications

## Installation & Setup

### Prerequisites
- Node.js (v16 or higher)
- Python (v3.8 or higher)
- PostgreSQL
- Google Cloud Platform account (for OAuth)

### Backend Setup

1. **Clone the repository**
```bash
git clone <repository-url>
cd todo-app/backend
```

2. **Create and activate virtual environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Configure environment variables**
Create a `.env` file in the backend directory:
```env
# Database
DATABASE_URL=postgresql://username:password@localhost:5432/todoapp

# JWT Secret
SECRET_KEY=your-super-secret-key-change-this-in-production

# Google OAuth
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret

# GitHub OAuth
GITHUB_CLIENT_ID=your_github_client_id
GITHUB_CLIENT_SECRET=your_github_client_secret

# URLs
FRONTEND_URL=http://localhost:3000
BACKEND_URL=http://localhost:8000

# AI API
GROQ_API_KEY=your_groq_api_key
```

5. **Run the backend server**
```bash
uvicorn main:app --reload
```

### Frontend Setup

1. **Navigate to frontend directory**
```bash
cd ../frontend
```

2. **Install dependencies**
```bash
npm install
```

3. **Configure environment variables**
Create a `.env.local` file in the frontend directory:
```env
NEXT_PUBLIC_API_URL=http://localhost:8000
NEXT_PUBLIC_GOOGLE_CLIENT_ID=your_google_client_id
```

4. **Run the development server**
```bash
npm run dev
```

## OAuth Configuration

### Google OAuth Setup

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project or select an existing one
3. Enable the Google People API
4. Go to "Credentials" and create an OAuth 2.0 Client ID
5. Set the authorized redirect URIs:
   - `http://localhost:8000/auth/google/callback`
6. Add the client ID and secret to your `.env` files

### GitHub OAuth Setup

1. Go to GitHub Settings > Developer settings > OAuth Apps
2. Create a new OAuth App
3. Set the homepage URL to your frontend URL
4. Set the authorization callback URL to `http://localhost:8000/auth/github/callback`
5. Add the client ID and secret to your `.env` files

## API Endpoints

### Authentication
- `POST /auth/register` - Register a new user
- `POST /auth/login` - Login with email and password
- `GET /auth/google` - Initiate Google OAuth flow
- `GET /auth/google/callback` - Handle Google OAuth callback
- `GET /auth/github` - Initiate GitHub OAuth flow
- `GET /auth/github/callback` - Handle GitHub OAuth callback
- `GET /auth/me` - Get current user info

### Tasks
- `GET /api/tasks` - Get user's tasks
- `POST /api/tasks` - Create a new task
- `GET /api/tasks/{task_id}` - Get a specific task
- `PUT /api/tasks/{task_id}` - Update a task
- `DELETE /api/tasks/{task_id}` - Delete a task
- `PATCH /api/tasks/{task_id}/complete` - Toggle task completion

### Chat
- `POST /api/chat` - Send message to AI assistant

## Database Schema

The application uses PostgreSQL with the following main tables:

### Users
- id (UUID)
- email (unique)
- hashed_password
- provider (email/google/github)
- first_name, last_name
- bio, location, timezone
- theme_preference
- created_at, last_login

### Tasks
- id (UUID)
- user_id (foreign key to users)
- title, description
- completed (boolean)
- priority (enum: low, medium, high)
- tags (JSON array)
- created_at, updated_at

### Conversations & Messages
- Support for AI chat conversations
- Message history for each conversation

## Environment Variables

### Backend (.env)
- `DATABASE_URL` - PostgreSQL connection string
- `SECRET_KEY` - JWT secret key
- `GOOGLE_CLIENT_ID` - Google OAuth client ID
- `GOOGLE_CLIENT_SECRET` - Google OAuth client secret
- `GITHUB_CLIENT_ID` - GitHub OAuth client ID
- `GITHUB_CLIENT_SECRET` - GitHub OAuth client secret
- `FRONTEND_URL` - Frontend application URL
- `BACKEND_URL` - Backend application URL
- `GROQ_API_KEY` - Groq API key for AI integration

### Frontend (.env.local)
- `NEXT_PUBLIC_API_URL` - Backend API URL
- `NEXT_PUBLIC_GOOGLE_CLIENT_ID` - Google OAuth client ID

## Running the Application

1. Start the backend server:
```bash
cd backend
uvicorn main:app --reload
```

2. In a new terminal, start the frontend:
```bash
cd frontend
npm run dev
```

3. Access the application:
   - Frontend: http://localhost:3000
   - Backend API docs: http://localhost:8000/docs

## Troubleshooting

### Common Issues

1. **CORS errors**: Ensure your frontend URL is included in the backend's CORS configuration
2. **OAuth redirect issues**: Verify that the redirect URI matches exactly what's registered in Google/GitHub
3. **Database connection**: Make sure PostgreSQL is running and credentials are correct
4. **Authentication failures**: Check that JWT secrets match between environments

### OAuth Callback Issues

If OAuth isn't working properly:
1. Verify the redirect URIs in your Google/GitHub developer console
2. Check that `FRONTEND_URL` and `BACKEND_URL` are correctly set in your environment
3. Ensure the callback endpoints are accessible at the expected URLs

## Development

### Adding New Features

1. Create new API endpoints in the FastAPI backend
2. Add corresponding frontend components
3. Update the database schema if needed
4. Write tests for new functionality
5. Update this README as needed

### Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Deployment

### Backend Deployment
- Ensure environment variables are properly configured
- Use a production-ready database (PostgreSQL)
- Set up proper SSL certificates
- Use a WSGI server like Gunicorn in production

### Frontend Deployment
- Build the application: `npm run build`
- Serve the static files with a web server
- Ensure API endpoints are correctly configured for production

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- FastAPI for the excellent web framework
- Next.js for the React framework
- PostgreSQL for the reliable database
- Google and GitHub for OAuth services
- Groq for AI inference capabilities