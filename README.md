# Little Lemon – Django REST Framework Capstone

A small Django restaurant project with a server-rendered homepage, menu API, table-booking API, user registration, token authentication, role-aware permissions, MySQL configuration, and automated API tests.

See **Readme.txt** for setup instructions and the API endpoint list for peer reviewers.

## Quick start

```bash
python -m venv .venv
# Windows: .venv\\Scripts\\activate
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

By default the project uses SQLite for a quick local run. To use MySQL, copy `.env.example` to `.env`, set valid database credentials, keep `DB_ENGINE=mysql`, create the database, then run migrations. Never commit `.env`.

## Tests

```bash
python manage.py test
```

## Main endpoints

- `GET /` – HTML homepage
- `/restaurant/menu/` – menu list/create and filtering/search/ordering/pagination
- `/restaurant/menu/<id>/` – individual menu item
- `/restaurant/booking/tables/` – authenticated table bookings
- `POST /auth/users/` – user registration
- `POST /token/login/` – token login

See **Readme.txt** for request examples and permission details.
