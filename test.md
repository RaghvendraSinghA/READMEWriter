## AMA session Q&A

### Q1. What is ORM? ( Aditya Sharma )
  - ORM stands for Object-Relational Mapping.
  - It allows us to interact with a database using programming language objects instead of writing SQL queries directly.
  - In Django, Django ORM lets us work with database tables using Python models.
  - Example:
    ```python
    User.objects.all()
    ```
    This internally generates a SQL query to retrieve users.

### Q2. What is an event listener? ( Alok kumar )
  - An event listener is a function that waits for a specific event to occur on an element.
  - When the event occurs, the function is executed.
  - Example:
    ```javascript
    button.addEventListener("click", function () {
        console.log("Button clicked");
    });
    ```
  - Here, `click` is the event and the function is the event handler.

### Q3. What is a self join in SQL? ( Amit Chandra Dey )
  - A self join is when a table is joined with itself.
  - It is useful when records in the same table are related to each other.
  - Example: an employee table can contain both employees and their managers.
  - We can use a self join to find each employee's manager.

### Q4. What is SQLite in Django? ( Atul Kumar )
  - SQLite is a lightweight, file-based relational database.
  - Django uses SQLite as its default database when a project is created.
  - The database is usually stored in a file called `db.sqlite3`.
  - It is useful for development and small projects because it does not require a separate database server.

### Q5. What is `AbstractUser` in Django? ( Bokam Manikanta ) 
  - `AbstractUser` is a Django class that provides the fields and functionality of Django's default user model.
  - We can inherit from it to create a custom user model while keeping Django's built-in authentication features.
  - Example:
    ```python
    from django.contrib.auth.models import AbstractUser

    class User(AbstractUser):
        pass
    ```
  - We can then add our own fields or customize existing behavior.

### Q6. What is the difference between `HAVING` and `WHERE`? ( Pantham Adinarayana )
  - `WHERE` filters individual rows before grouping.
  - `HAVING` filters groups after `GROUP BY`.
  - Example:
    ```sql
    SELECT department, COUNT(*)
    FROM employees
    WHERE salary > 30000
    GROUP BY department
    HAVING COUNT(*) > 5;
    ```
  - Here, `WHERE` filters employees based on salary, while `HAVING` filters departments based on the number of employees.

### Q7. What is a migration in Django? ( Rahul Raj )
  - A migration is Django's way of tracking and applying changes made to models to the database schema.
  - When we change a model, we create a migration:
    ```bash
    python manage.py makemigrations
    ```
  - Then we apply the migration to the database:
    ```bash
    python manage.py migrate
    ```
  - For example, adding a new field to a model can create a migration that adds a new column to the database.

### Q8. What is `manage.py` in Django? ( Sai Ganesh Lanka )
  - `manage.py` is a command-line utility provided by Django for managing a Django project.
  - It sets up the project's settings and allows us to run Django management commands.
  - Examples:
    ```bash
    python manage.py runserver
    python manage.py makemigrations
    ```

### Q9. What happens when we create an app but do not add it to `INSTALLED_APPS`? ( Santosh Anil Gurkhe )
  - Django will not properly recognize the app as an installed application.
  - Its models will not be included when Django creates or detects migrations.
  - App-specific features such as models, admin configuration, and other Django application configuration may not work as expected.
  - Therefore, a Django app should normally be added to `INSTALLED_APPS` in `settings.py`.

### Q10. Why do we use `collectstatic`? ( Sibsankar Manna )
  - `collectstatic` collects static files from all installed Django apps and copies them into the directory specified by `STATIC_ROOT`.
  - It is mainly used when deploying a Django application.
  - Command:
    ```bash
    python manage.py collectstatic
    ```
  - It collects CSS, JavaScript, and image files into one location so a production web server can serve them efficiently.
