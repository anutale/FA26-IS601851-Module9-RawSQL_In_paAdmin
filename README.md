# FastAPI Calculator API

A small FastAPI application that exposes a simple calculator API and serves a browser-based calculator UI. The project includes unit, integration, and end-to-end tests, as well as Docker support for running the app with PostgreSQL and pgAdmin.

## Overview

This application demonstrates:

- FastAPI request handling and validation
- Arithmetic operations via reusable business logic functions
- Jinja2 HTML templating for a basic web front end
- API testing with pytest
- Browser automation using Playwright
- Containerized local development with Docker Compose

## Features

- Add, subtract, multiply, and divide endpoints
- Input validation for numeric values
- Clear error handling for invalid requests, including division by zero
- Simple HTML calculator interface at the root route
- Dockerized environment with PostgreSQL and pgAdmin
- CI/CD workflow for automated testing and image building

## Project Structure

```text
.
├── app/
│   └── operations/
│       └── __init__.py
├── templates/
│   └── index.html
├── tests/
│   ├── e2e/
│   │   ├── __init__.py
│   │   └── test_e2e.py
│   ├── integration/
│   │   ├── __init__.py
│   │   └── test_fastapi_calculator.py
│   ├── unit/
│   │   ├── __init__.py
│   │   └── test_calculator.py
│   ├── __init__.py
│   └── conftest.py
├── .github/
│   └── workflows/
│       └── test.yml
├── Dockerfile
├── docker-compose.yml
├── LICENSE
├── __init__.py
├── conftest.py
├── main.py
├── pytest.ini
├── requirements.txt
├── README.md
└── .gitignore
```

## Requirements

- Python 3.10 (the version used by CI and Docker; use it for the complete pinned dependency set)
- pip
- Optional: Docker Desktop and Docker Compose
- Optional for E2E tests: Playwright browsers

## Local Setup

1. Clone the repository.
2. Create and activate a virtual environment:

```bash
python3.10 -m venv .venv
source .venv/bin/activate   # On Windows use .venv\Scripts\activate
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

4. Start the application:

```bash
python main.py
```

or:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

5. Open the app in a browser:

- UI: http://127.0.0.1:8000/
- API docs: http://127.0.0.1:8000/docs

## API Endpoints

### Root page

- `GET /` — serves the HTML calculator front end

### Arithmetic operations

- `POST /add` — adds two numbers
- `POST /subtract` — subtracts two numbers
- `POST /multiply` — multiplies two numbers
- `POST /divide` — divides two numbers

Example request:

```json
{
  "a": 10,
  "b": 5
}
```

Example response:

```json
{
  "result": 15
}
```

Division by zero returns a 400 error with a message similar to:

```json
{
  "error": "Cannot divide by zero!"
}
```

## Docker Setup

This project includes a Docker Compose configuration that starts:

- the FastAPI app on port 8000
- PostgreSQL on port 5432
- pgAdmin on port 5050

Start everything with:

```bash
docker compose up --build
```

The app is available at:

- http://localhost:8000
- pgAdmin: http://localhost:5050

Default pgAdmin login:

- Email: admin@example.com
- Password: admin

## Running Tests

Install Playwright browsers if needed:

```bash
playwright install
```

Run the full suite:

```bash
pytest
```

Run a specific test group:

```bash
pytest tests/unit/
pytest tests/integration/
pytest tests/e2e/
```

## CI/CD

The repository includes a GitHub Actions workflow in `.github/workflows/test.yml` that:

- sets up Python 3.10
- installs dependencies
- runs unit, integration, and end-to-end tests
- builds the Docker image
- runs a Trivy vulnerability scan
- publishes Docker images on pushes to `main`

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
