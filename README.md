# Blog With Users (Flask)

A simple Flask blog example with user accounts, posts and comments. This repository demonstrates:

- Flask application structure (routes, templates, static files)
- Flask-Login for authentication
- Flask-WTF for forms + CKEditor integration
- Flask-SQLAlchemy (SQLAlchemy ORM) for models and relationships
- dotenv for local environment variables

**Quick Start**

- Create a virtual environment and install dependencies:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

- Create a `.env` file in the project root with at least:

```
SECRET_KEY=replace-with-a-secret
FLASK_DEBUG=1
PORT=5002
```

- Run the app:

```powershell
python main.py
```

Open http://127.0.0.1:5002 in your browser.

**Important files**

- `main.py` — application, models, routes, and configuration.
- `forms.py` — WTForms definitions used by routes and templates.
- `templates/` — Jinja2 templates (index, post, register, login, etc.).
- `static/` — CSS, JS, and images.
- `requirements.txt` — pinned Python dependencies.

**Environment & Security Notes**

- Do NOT commit your real `SECRET_KEY` or `.env` to GitHub. The repository contains a `.gitignore` which excludes `.env`, `.venv/`, and `*.db`.
- `posts.db` is the default SQLite file created when you run the app. If you already committed it earlier, remove it from git history or untrack it with `git rm --cached posts.db`.
- The app reads `FLASK_DEBUG` and `PORT` from environment variables; avoid running with `FLASK_DEBUG=1` in production.

**Database / Models**

- Models are defined with SQLAlchemy ORM: `User`, `BlogPost`, and `Comment`.
- Relationships use `ForeignKey` + `relationship(..., back_populates=...)`.
- When displaying author names in templates use `{{ post.author.name }}` or `{{ comment.author.name }}` — `post.author` is a `User` object.

**Common Commands**

```powershell
# install
python -m pip install -r requirements.txt
# run
$env:SECRET_KEY="dev-secret"; $env:FLASK_DEBUG=1; python main.py
# remove local db from git (if tracked)
git rm --cached posts.db
git add .gitignore
git commit -m "chore: ignore local env and db"
```

**Suggested commit message for recent changes**

`chore: fix route decorators and env-driven debug; add .gitignore`

If you want, I can also:

- Patch templates to use `post.author.name` and `comment.author.name` where needed.
- Add a short tests folder or a `README` run script.
- Create a `Procfile` or a simple Gunicorn example for deployment.
