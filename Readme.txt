LITTLE LEMON – DJANGO REST FRAMEWORK CAPSTONE
================================================

PROJECT OVERVIEW
----------------
This project is a Django restaurant website and REST API. It includes a server-rendered homepage, menu item endpoints, table booking endpoints, user registration, token authentication, MySQL configuration, and unit tests.

IMPORTANT SETUP
---------------
1. Install Python 3.10 or later.
2. Create and activate a virtual environment.
3. Install dependencies:
       pip install -r requirements.txt
4. Copy .env.example to .env and update the MySQL database name, username, password, host, and port.
5. Create the MySQL database (for example, littlelemon) before migrating.
6. Run:
       python manage.py makemigrations
       python manage.py migrate
       python manage.py createsuperuser
       python manage.py runserver

The settings file supports MySQL through DB_ENGINE=mysql. For a quick local smoke test without a MySQL server, remove/rename .env or set DB_ENGINE=sqlite; the project then uses SQLite. Do not commit .env or real credentials.

API PATHS FOR PEER TESTING
--------------------------
HTML HOMEPAGE
GET     /

MENU ITEMS
GET     /restaurant/menu/
POST    /restaurant/menu/                 (Manager or staff)
GET     /restaurant/menu/<id>/
PUT     /restaurant/menu/<id>/            (Manager or staff)
PATCH   /restaurant/menu/<id>/            (Manager or staff; e.g. featured)
DELETE  /restaurant/menu/<id>/            (Manager or staff)

Menu query examples:
GET     /restaurant/menu/?category=Salads
GET     /restaurant/menu/?search=salad
GET     /restaurant/menu/?ordering=price
GET     /restaurant/menu/?page=2

TABLE BOOKINGS
GET     /restaurant/booking/tables/       (Authenticated; customer sees own bookings)
POST    /restaurant/booking/tables/       (Authenticated; owner is assigned server-side)
GET     /restaurant/booking/tables/<id>/  (Owner, Manager, or staff)
PUT     /restaurant/booking/tables/<id>/  (Owner, Manager, or staff)
PATCH   /restaurant/booking/tables/<id>/  (Owner, Manager, or staff)
DELETE  /restaurant/booking/tables/<id>/  (Owner, Manager, or staff)

USER REGISTRATION AND TOKEN AUTHENTICATION
POST    /auth/users/
POST    /token/login/
POST    /api-token-auth/                  (Alias for token login)

Example registration JSON:
{
  "username": "customer1",
  "email": "customer1@example.com",
  "password": "Use-a-strong-password"
}

Example token login JSON:
{
  "username": "customer1",
  "password": "Use-a-strong-password"
}

Include the returned token in protected requests:
Authorization: Token <token-value>

EXAMPLE MENU ITEM JSON
----------------------
{
  "title": "Greek Salad",
  "price": "12.50",
  "inventory": 20,
  "description": "Fresh salad with herbs and feta.",
  "category": "Salads",
  "featured": true
}

EXAMPLE BOOKING JSON
--------------------
{
  "name": "Alex",
  "no_of_guests": 2,
  "booking_date": "2026-11-10T19:00:00+05:30"
}

PERMISSIONS
-----------
- Menu reads are public. Menu creation, updating, and deletion require a Manager group member or Django staff/superuser.
- Booking endpoints require authentication. Customers can see and manage only their own bookings. Managers and staff can manage all bookings.
- The booking owner is assigned from the authenticated request user; clients cannot choose another user's ID.

TESTS
-----
Run the automated tests with:
    python manage.py test

For tests without a MySQL service, configure DB_ENGINE=sqlite in .env. For peer review against MySQL, configure DB_ENGINE=mysql and valid local MySQL credentials.

GIT SUBMISSION
--------------
The Coursera instructions ask for a GitHub repository URL. After checking the project, initialize Git, commit the files, push the repository to GitHub, and submit the repository URL in Coursera. Do not commit .env, passwords, or secret keys.
