# Git2Know

**Explore GitHub developers and repositories with AI-powered summaries and interactive Q&A.**

Git2Know is a web application that helps users understand GitHub developers and their repositories. It retrieves repository information from GitHub and uses an AI model to generate summaries and answer questions about developers and projects.

## Features

* **Developer Summary:** Generate summaries of a developer's skills, technologies, and projects.
* **Repository Summary:** Get an overview of a repository's purpose, features, and technologies based on its README.
* **AI-Powered Q&A:** Ask questions about GitHub developers and repositories.
* **Conversation History:** Maintain context across questions during a conversation.
* **GitHub Integration:** Retrieve repository information using the GitHub REST API.
* **Caching:** Store retrieved information and conversation history in Redis to reduce repeated requests.
* **Markdown Rendering:** Display AI-generated responses in a readable format.

## Tech Stack

### Frontend

* React
* Vite
* Tailwind CSS
* Axios
* React Markdown

### Backend

* Python
* Flask
* Flask-CORS
* Requests

### APIs and Services

* GitHub REST API
* Groq API for AI-generated responses
* Redis for caching

## Project Structure

```text
git2know/
├── backend/
│   ├── main.py
│   ├── .env
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   └── assets/
│   ├── package.json
│   └── index.html
└── README.md
```

## Prerequisites

Install the following before running the project:

* Python 3.10 or later
* Node.js and npm
* A GitHub API token
* A Groq API key
* A Redis instance

## Installation and Setup

### 1. Clone the Repository

```bash
git clone <your-repository-url>
cd git2know
```

### 2. Set Up the Backend

Navigate to the backend directory:

```bash
cd backend
```

Create a virtual environment:

```bash
python -m venv venv
```

Activate it on Windows:

```powershell
.\venv\Scripts\Activate.ps1
```

Install the Python dependencies:

```bash
pip install -r requirements.txt
```

### 3. Configure Environment Variables

Create a `.env` file inside the `backend` directory:

```env
GROQ_API_KEY=your_groq_api_key
GITHUB_API_KEY=your_github_api_key
REDIS_URL=your_redis_connection_url
```

Replace the placeholders with your actual credentials.

**Never commit your `.env` file or expose API keys publicly.**

### 4. Run the Backend

From the `backend` directory, run:

```bash
python main.py
```

The Flask server starts at:

```text
http://127.0.0.1:5000
```

### 5. Set Up the Frontend

Open a separate terminal:

```bash
cd frontend
npm install
npm run dev
```

Open the local URL displayed by Vite, usually:

```text
http://localhost:5173
```

## How to Use

1. Open Git2Know in your browser.
2. Navigate to Developer Info or Repository Info.
3. Enter a GitHub username or repository details.
4. Generate an AI-powered summary.
5. Open the Q&A page.
6. Select Developer or Repository mode.
7. Set the username or repository.
8. Ask questions and view the generated responses.

## Backend API Endpoints

| Method | Endpoint                          | Description                                  |
| ------ | --------------------------------- | -------------------------------------------- |
| GET    | `/devinfo/<username>`             | Generate a developer summary                 |
| GET    | `/repoinfo/<username>/<reponame>` | Generate a repository summary                |
| GET    | `/load/<username>`                | Retrieve and cache developer repository data |
| GET    | `/load/<username>/<reponame>`     | Retrieve and cache repository README data    |
| POST   | `/chatdev`                        | Ask questions about a developer              |
| POST   | `/chatrepo`                       | Ask questions about a repository             |

### Example Q&A Request

**Endpoint:** `POST /chatdev`

Request body:

```json
{
  "username": "octocat",
  "prompt": "What programming languages does this developer use?"
}
```

Repository Q&A uses the following request body:

```json
{
  "username": "octocat",
  "repository": "Hello-World",
  "prompt": "What is this project about?"
}
```

## AI Integration

Git2Know uses an AI API to generate summaries and answer questions using retrieved GitHub data.

The backend sends relevant developer or repository information to the AI model and returns the generated response to the frontend.

The configured model and API provider can be changed through the backend configuration.

## Caching

Redis stores retrieved developer or repository data and conversation history with a limited expiration time. This helps avoid repeatedly retrieving the same information during a session.

## Error Handling

The application handles errors such as:

* Invalid GitHub usernames or repositories
* Missing cached data
* API request failures
* AI provider quota limits
* Redis connection or caching failures

## Security

* Store API credentials in environment variables.
* Keep `.env` out of version control.
* Do not expose secret keys in frontend code.
* Use appropriate API quotas and rate limits.

## Future Improvements

* Add support for comparing multiple repositories.
* Improve error messages and loading indicators.
* Add user authentication and persistent chat history.
* Introduce repository analytics and language statistics.
* Add automated tests for frontend and backend endpoints.

## License

Add the license that applies to your project.
