# url-shortener

URL shortener with click tracking. Backend in FastAPI and PostgreSQL, frontend in React + TypeScript coming later.

Still a work in progress: the API is being built and there is no frontend yet.

## Stack

- Python, FastAPI, SQLAlchemy
- PostgreSQL 16 (via Docker Compose)
- React, TypeScript and Vite (planned)

## Endpoints

- `POST /api/links`: create a short link, with an optional custom alias
- `GET /{code}`: redirect to the original URL and count the click
- `GET /api/links/{code}/stats`: link info and click count
- `GET /health`: health check

Swagger docs at `http://localhost:8000/docs` while the API is running.

## Structure

```
backend/app/
├── core/           settings, db connection, exceptions
├── models/         SQLAlchemy models
├── repositories/   data access
├── routers/        HTTP endpoints
├── schemas/        Pydantic schemas
├── services/       business logic
└── main.py
```

Flow: router -> service -> repository -> database.

## Running locally

You need Python 3.12+ and Docker.

```bash
git clone https://github.com/dev-brunoantunes/url-shortener.git
cd url-shortener
cp .env.example .env    # Windows: copy .env.example .env
```

Edit `.env` and change the password, then start the database:

```bash
docker compose up -d
```

Create a virtualenv and install the dependencies:

```bash
python -m venv .venv
source .venv/bin/activate    # Windows: .venv\Scripts\Activate.ps1
pip install -r backend/requirements.txt
```

Run the API:

```bash
cd backend
uvicorn app.main:app --reload
```

## Roadmap

- [x] Project structure
- [x] Postgres with Docker Compose
- [ ] Create links (with custom alias)
- [ ] Redirect + click tracking
- [ ] Stats endpoint
- [ ] Alembic migrations
- [ ] Tests (pytest)
- [ ] CI (GitHub Actions)
- [ ] Frontend
- [ ] Dockerize everything
- [ ] Deploy

## License

MIT