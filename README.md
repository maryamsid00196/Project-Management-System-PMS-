# Project Management System (PMS)

A Django-based web application for managing projects, teams, and roles. Users can register and log in as **Project Heads**, **Clients**, or **Assigners**, create projects, and access role-specific dashboards.

## Features

- **Role-based access**: Project Head, Assigner, Assignee, and Client
- **Assignee roles**: Developer, Manager, Designer, Tester
- **Project creation**: Add projects with name, description, cost, time period, and assignments
- **Registration & login** for Project Heads, Clients, and Assigners
- **Bootstrap 4** UI with responsive layout

## Project Structure

```
tech pack/
└── ProjectManagementSystem/
    ├── manage.py           # Django CLI
    ├── PMS/                # Project settings
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
    ├── website/            # Main app (views, urls, models)
    └── template/           # HTML templates
        ├── index.html      # Home / landing
        ├── Project_Head.html, Assigner.html, client.html
        ├── PHlogin.html, Alogin.html, Clogin.html
        ├── PHpage.html, Apage.html, Cpage.html
        └── developer.html, manager.html, designer.html, tester.html
```

## Requirements

- **Python 3** (Django 4.1.5)
- **MySQL** server with a database named `pms`
- **mysqlclient** (or `mysql-connector-python`) for database access

## Setup

1. **Clone or open the project** and go to the Django project folder:
   ```bash
   cd ProjectManagementSystem
   ```

2. **Create a virtual environment** (recommended):
   ```bash
   python -m venv venv
   venv\Scripts\activate
   ```

3. **Install dependencies**:
   ```bash
   pip install django mysqlclient
   ```

4. **Configure the database**  
   The app uses MySQL. In `PMS/settings.py` you can keep SQLite for quick testing, but the `website` views are written for MySQL. Ensure MySQL is running and you have a database named `pms`. Update the database credentials in `website/views.py` to match your MySQL user and password (use environment variables or a config file in production; avoid committing passwords).

5. **Create MySQL tables**  
   Create the tables expected by the app (e.g. `project_head`, `assigner`, `client`, `project`) with the same column names used in the views.

6. **Register the app** (if not already):  
   In `PMS/settings.py`, add `'website'` to `INSTALLED_APPS` and set `'DIRS': [BASE_DIR / 'template']` (or the path to your template folder) in `TEMPLATES` so Django can find the HTML files.

7. **Include website URLs**  
   In `PMS/urls.py`, add:
   ```python
   path('', include('website.urls')),
   ```

8. **Run migrations** (for Django auth and any Django models):
   ```bash
   python manage.py migrate
   ```

9. **Start the development server**:
   ```bash
   python manage.py runserver
   ```

   Open **http://127.0.0.1:8000/** in your browser.

## Usage

- **Home**: Landing page with links to different role entry points.
- **All entries**: Hub to register or log in as Project Head, Assigner, or Client.
- **Project Head**: Register, log in, create projects, and view your dashboard.
- **Assigner**: Register, log in, and access assigner dashboard.
- **Client**: Register, log in, and access client dashboard.
- **Assignee**: Navigate to Developer, Manager, Designer, or Tester pages.

## Security Note

Before deploying or sharing the project:

- Do **not** commit real database passwords. Use environment variables or a local config file and add that file to `.gitignore`.
- Set `DEBUG = False` and configure `ALLOWED_HOSTS` and static file serving for production.
- Change `SECRET_KEY` in `settings.py` for production.

## License

Use and modify as needed for your organization.
