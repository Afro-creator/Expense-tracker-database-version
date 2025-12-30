# Expense Tracker (SQLite + databases + FastAPI)

Minimal async expense-tracker API using SQLite and the `databases` library. The main application is `Practice.py` (FastAPI app). Data is stored in `expenses.db` next to the script.

## Requirements
- Python 3.8+
- Recommended packages:
  - fastapi
  - uvicorn[standard]
  - databases[sqlite]
  - SQLAlchemy
  - pydantic

## Setup (Windows)
Open PowerShell in the folder containing `Practice.py` (example path shown):

1. Create and activate a virtual environment
   ```powershell
   python -m venv venv
   .\venv\Scripts\activate

2. Installing dependencies
  pip install fastapi uvicorn[standard] databases[sqlite] SQLAlchemy pydantic

(Or add a requirements.txt and run pip install -r requirements.txt.)

Run
Start the server with uvicorn (module name is the filename without .py):
python -m uvicorn Practice:app --reload --host 127.0.0.1 --port 8000

Open interactive docs: http://127.0.0.1:8000/docs

API Endpoints (summary)
POST /expenses — create an expense
Body: { description, amount, category, incurred_at }
GET /expenses — list expenses (supports limit and offset)
GET /expenses/{id} — get a single expense
PATCH /expenses/{id} — update fields for an expense
DELETE /expenses/{id} — delete an expense
GET /reports/category_totals — totals grouped by category

Example curl (create)
curl -X POST "http://127.0.0.1:8000/expenses" -H "Content-Type: application/json" -d ^
'{"description":"Coffee","amount":3.50,"category":"Food","incurred_at":"2025-11-27T09:00:00"}'

Data file
SQLite DB file: expenses.db (created automatically next to Practice.py)
SQLAlchemy table definitions live in the module-level code in Practice.py (or split into db.py / models.py if refactoring).

Notes & recommendations
Current code creates tables on startup and uses databases for async DB access.
For production: enable proper migrations (Alembic), use atomic writes, and add input validation and tests.
Avoid running multiple processes writing to the same SQLite DB without proper configuration.