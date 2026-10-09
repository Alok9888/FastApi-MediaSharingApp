FastAPI Media Sharing App
A FastAPI backend with a Streamlit frontend for user registration and authentication, media uploads through ImageKit, and a feed of uploaded posts.
Features
- User registration and login using FastAPI Users and JWT authentication
- Authenticated user profile access
- Media upload through ImageKit
- Post metadata stored in a database
- Feed endpoint for retrieving posts
- Delete endpoint that checks post ownership
- Streamlit UI for interacting with the API
Tech Stack
- Backend: FastAPI, Uvicorn
- Authentication: FastAPI Users, JWT
- Database: SQLAlchemy with SQLite for local development
- Media storage: ImageKit
- Frontend: Streamlit
- Validation: Pydantic
Project Structure
FastAPI11/
├── app/
│   ├── __init__.py
│   ├── app.py
│   ├── db.py
│   ├── users.py
│   ├── schemas.py
│   └── images.py
├── main.py
├── frontend.py             # Replace with your actual Streamlit filename
├── requirements.txt
├── README.md
├── .gitignore
└── .env                    # Local only; never commit this file
Prerequisites
- Python 3.11 or a compatible Python version
- An ImageKit account and private key
- Git (if cloning or contributing through GitHub)
Setup
1. Clone the repository
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd FastAPI11
2. Create and activate a virtual environment
Windows PowerShell:
python -m venv .venv
.\.venv\Scripts\Activate.ps1
macOS/Linux:
python3 -m venv .venv
source .venv/bin/activate
3. Install dependencies
python -m pip install -r requirements.txt
4. Configure environment variables
Create a local .env file in the project root. Add the credentials required by app/images.py, for example:
IMAGEKIT_PRIVATE_KEY=your_imagekit_private_key
IMAGEKIT_URL=your_imagekit_url_endpoint
Keep .env private. Do not commit credentials to GitHub.
Move the JWT secret in app/users.py into an environment variable before publishing the project. Use a long, random secret and never expose it in source control. Ensure the code reads that environment variable; adding it to .env alone is not enough.
5. Run the FastAPI backend
From the project root:
python main.py
The API should be available at:
- API base: http://localhost:8000
- Interactive API docs: http://localhost:8000/docs
6. Run the Streamlit frontend
In a second terminal, activate the same virtual environment, then run:
python -m streamlit run frontend.py
Replace frontend.py with the actual name of your Streamlit file if it differs.
Main API Routes
The routes below reflect the current project design; confirm exact prefixes and methods in app/app.py and app/users.py if you change them.
Purpose	Route
Register	POST /auth/register
Log in and obtain JWT	POST /auth/jwt/login
Current user	GET /users/me
Upload media	POST /upload
View feed	GET /feed
Delete a post	DELETE /posts/{id}


FastAPI Users may expose additional password-reset and verification routes depending on the router configuration.
Authentication
Routes that require a signed-in user need a valid JWT access token. Log in first, then send the token as a bearer token in the Authorization header:
Authorization: Bearer <your_access_token>
Do not share real access tokens or commit them to the repository.
Database Notes
The project uses SQLite for local development and creates tables when the application starts. The local database file is intentionally excluded from Git. For a deployed application, review database compatibility, migrations, and persistent storage before deployment.
Security Notes
- Never commit .env, private API keys, JWT secrets, passwords, or access tokens.
- Load secrets from environment variables.
- Use a different strong JWT secret outside local development.
- Configure HTTPS and appropriate CORS settings before public deployment.
- Validate uploads, enforce sensible file-size/type limits, and handle external storage errors.
- Review database and authentication configuration before production use.
Current Scope
This README describes the project's intended features and setup. Test each route and the ImageKit upload flow in your environment before presenting the application as fully working.
License
Add a license if you intend to make this project open source.
