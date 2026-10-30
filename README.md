<p align="center">
  <img src="assets/traction-api-mark.png" alt="Traction API endpoints and database mark" width="200" />
</p>

<h1 align="center">Traction Backend</h1>

<p align="center">FastAPI and PostgreSQL API for the Traction client. The service includes routes for authentication, projects, chat, documents, public project pages, and sharing. The frontend is in <a href="https://github.com/AbhiramVSA/traction-ai">traction-ai</a>.</p>

## Stack

| Area | Technology |
| --- | --- |
| API | FastAPI, Python 3.12+ |
| Database | PostgreSQL, SQLModel, asyncpg |
| Migrations | Alembic |
| Authentication | JWT and Google OAuth via Authlib |
| AI | OpenAI and Pydantic AI |
| Environment | `uv` |

## Local setup

Install the locked dependencies from the repository root:

```bash
uv sync --locked
```

Start a PostgreSQL database. This repository does not include a Docker Compose file.

Create a root `.env` file. The settings module reads it when you run the API from `backend/`.

```env
MODE=development
SECRET_KEY=replace-with-a-local-secret
DATABASE_USER=postgres
DATABASE_PASSWORD=replace-with-your-local-password
DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_NAME=app_db
OPENAI_API_KEY=replace-with-your-key
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
GOOGLE_REDIRECT_URI=
```

The database must be available before the API starts. Apply migrations, then start the server:

```bash
cd backend
uv run --project .. alembic upgrade head
uv run --project .. uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```

Open the API docs at `http://127.0.0.1:8000/docs`. The root route and `/db_check` provide basic API and database status responses.

## Repository layout

- `backend/app/api/v1/routers/` — API route groups.
- `backend/app/models/` and `backend/app/schemas/` — database models and request/response schemas.
- `backend/alembic/` — database migrations.
- `backend/alembic.ini` — Alembic settings.
- `pyproject.toml` and `uv.lock` — dependency and Python project settings.
