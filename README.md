# Todo Full-Stack Web Application

A full-stack todo application with user authentication, task management, and responsive UI.

## Features

- User registration and authentication
- Secure JWT-based authentication
- Create, read, update, and delete tasks
- User data isolation (each user can only access their own tasks)
- Responsive web interface
- Persistent storage with Neon PostgreSQL

## Tech Stack

### Backend
- **Framework**: FastAPI (Python)
- **Database**: PostgreSQL (compatible with Neon)
- **ORM**: SQLModel
- **Authentication**: JWT with secure token handling
- **Server**: Uvicorn (ASGI server)

### Frontend
- **Framework**: React
- **Styling**: Tailwind CSS
- **Routing**: React Router
- **HTTP Client**: Axios

### Infrastructure
- **Containerization**: Docker and Docker Compose
- **Environment**: Node.js (for frontend), Python 3.9+ (for backend)

## Prerequisites

- Docker and Docker Compose
- Node.js v18+ (for local development)
- Python 3.9+ (for local development)

## Getting Started

### Using Docker (Recommended)

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd todo-fullstack
   ```

2. Copy the example environment file:
   ```bash
   cp .env.example .env
   ```

3. Update the `.env` file with your configuration (especially the database credentials and secret key)

4. Build and start the services:
   ```bash
   docker-compose up --build
   ```

5. The application will be available at:
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:8000
   - Backend API Docs: http://localhost:8000/docs

### Local Development

#### Backend Setup

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```

2. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Set up environment variables:
   ```bash
   cp ../.env.example .env
   # Update the .env file with your configuration
   ```

5. Run the application:
   ```bash
   uvicorn src.main:app --reload --port 8000
   ```

#### Frontend Setup

1. Navigate to the frontend directory:
   ```bash
   cd frontend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Set up environment variables:
   ```bash
   cp ../.env.example .env
   # Update the .env file with your configuration
   ```

4. Start the development server:
   ```bash
   npm run dev
   ```

## API Endpoints

### Authentication

- `POST /api/register` - Register a new user
- `POST /api/login` - Authenticate a user and get JWT token

### Tasks

All task endpoints require authentication via JWT token in the Authorization header.

- `GET /api/{user_id}/tasks` - Get all tasks for a user
- `POST /api/{user_id}/tasks` - Create a new task for a user
- `GET /api/{user_id}/tasks/{task_id}` - Get a specific task
- `PUT /api/{user_id}/tasks/{task_id}` - Update a specific task
- `DELETE /api/{user_id}/tasks/{task_id}` - Delete a specific task
- `PATCH /api/{user_id}/tasks/{task_id}/complete` - Mark a task as completed

## Environment Variables

### Backend (.env)

- `DATABASE_URL` - PostgreSQL database URL
- `SECRET_KEY` - Secret key for JWT signing (use a strong secret in production)
- `ACCESS_TOKEN_EXPIRE_MINUTES` - JWT token expiration time

### Frontend (.env)

- `REACT_APP_API_BASE_URL` - Base URL for the backend API

## Security

- Passwords are securely hashed using bcrypt
- JWT tokens are used for authentication
- All API endpoints validate user authorization
- Users can only access their own data

## Development

### Backend Development

Backend code is located in the `backend/src/` directory with the following structure:
- `models/` - SQLModel database models
- `services/` - Business logic services
- `api/routes/` - API route handlers
- `auth/` - Authentication utilities
- `database/` - Database connection setup

### Frontend Development

Frontend code is located in the `frontend/src/` directory with the following structure:
- `components/` - Reusable React components
- `pages/` - Page-level components
- `services/` - API and authentication services
- `utils/` - Utility functions

## Deployment

The application is designed to be deployed using Docker containers. The `docker-compose.yml` file defines the services needed for the application:

- Backend API service
- Frontend web service
- PostgreSQL database service

Update the environment variables in `docker-compose.yml` with production values before deploying.

## License

This project is licensed under the MIT License.