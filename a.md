## AMA session

### 1. (Aditya Sharma) — Explain `async` and `await`

`async` and `await` are used to work with asynchronous operations in JavaScript.

- `async` makes a function return a Promise.
- `await` pauses the execution inside an `async` function until the Promise is settled.
- `await` makes asynchronous code easier to read and understand, Code looks like synchronous.

Example:

```javascript
async function getData() {
    const response = await fetch("https://example.com/data");
    const data = await response.json();

    console.log(data);
}
```

Here, `await` waits for the `fetch()` operation to complete before moving to the next line and prints data.

---

### 2. (Alok Kumar) — What is a form in Django?

A form in Django is used to collect and validate data from users.

Django provides `forms.Form` and `forms.ModelForm`.

Example:

```python
from django import forms

class UserForm(forms.Form):
    username = forms.CharField()
    email = forms.EmailField()
    age = forms.IntegerField()
```

When the user submits the form, Django can validate the submitted data using:

```python
form.is_valid()
```

A `ModelForm` can also be used to create or update database objects directly from a form.    
We can also attach CSRF token inside it.

---

### 3. (Amit Chandra Dey) — What are validators?

Validators are functions that check whether a value satisfies a particular condition.

If the value is invalid, the validator raises a `ValidationError`.

Example:

```python
from django.core.validators import MinValueValidator
from django.db import models

class Product(models.Model):
    price = models.IntegerField(
        validators=[MinValueValidator(1)]
    )
```

Here, the price must be at least 1.

Validators are commonly used to validate form fields and model fields.

---

### 4. (Atul Kumar) — What is the new HTTP method?

The new HTTP QUERY method, officially standardized in June 2026 under RFC 10008,    
is the first major addition to standard HTTP verbs since PATCH in 2010.    
It is specifically designed to solve a 16-year-old dilemma for API developers:   
how to execute complex, heavy, or structured database lookups safely without abusing GET or POST.

The Problem It Solves
Historically, if you wanted to perform a complex search (like a dashboard with multi-nested filters,     
arrays, or AI/LLM semantic data retrieval), you had two imperfect options:

1. GET with query parameters: URLs have a practical limit (usually around 8 KB),
   making deeply nested arrays painful to encode. Sensitive data is also exposed in browser histories and proxy logs.    
3. GET with a request body: While tempting, the HTTP specification doesn't formally support this.
    Many clients, firewalls, and CDNs completely drop or reject GET requests containing a body.
5. POST requests: Developers routinely use POST for heavy searches just to pass a JSON body.
   However, POST is semantically a state-changing operation. It is not inherently safe, idempotent, or easily cacheable out of the box.


---

### 5. (Bokam Manikanta) — What is callback hell?

Callback hell happens when multiple asynchronous operations are nested inside callbacks,      
making the code difficult to read and maintain.  

Example:

```javascript
getUser(function(user) {
    getPosts(user, function(posts) {
        getComments(posts, function(comments) {
            getLikes(comments, function(likes) {
                console.log(likes);
            });
        });
    });
});
```

The deeply nested structure makes the code difficult to understand.

Promises and `async/await` are commonly used to make this code cleaner.

---

### 6. (Pantham Adinarayana) — What does `lang="en"` mean in HTML?

`lang="en"` tells the browser that the main language of the HTML document is English.

Example:

```html
<html lang="en">
```

Here:

- `lang` is an HTML attribute.
- `en` represents English.

It helps browsers, screen readers, search engines, and other tools understand the language of the page.

For example:

```html
<html lang="hi">
```

means that the document is primarily in Hindi.

---

### 7. (Rahul Raj) — What is a framework?

A framework is a collection of tools, libraries, and predefined structures that helps developers    
build applications faster and in an organized way.

For example:

- Django → Python web framework
- React → JavaScript library for building user interfaces
- Express → Node.js web framework

Django provides features such as:

- URL routing
- Database ORM
- Authentication
- Forms
- Middleware
- Security features
- Template system

Instead of building these features from scratch, developers can use the features provided by the framework.
Framework also controls and execute developer code by themselves. Framework controls the code.


---

### 8. (Sai Ganesh Lanka) — How do you get all data from the shell for a particular object?

In Django shell, we can use the model's manager to retrieve objects from the database.

For example:

```python
from ipl.models import Match
```

To get all objects:

```python
Match.objects.all()
```

To get a particular object:

```python
match = Match.objects.get(id=1)
```

To see all fields/data of that object:

```python
match.__dict__
```


---

### 9. (Santosh Anil Gurkhe) — Why do we inherit from `models.Model`?

We inherit from `models.Model` because Django needs to know that our class is a Django model.
Without inheriting from `models.Model`, Django would treat `User` as a normal    
Python class rather than a Django database model.

Example:

```python
from django.db import models

class User(models.Model):
    username = models.CharField(max_length=100)
    email = models.EmailField()
```

By inheriting from `models.Model`, Django provides features such as:

- Mapping the class to a database table
- Database fields
- Primary keys
- Querying through the ORM
- Saving objects
- Updating objects
- Deleting objects

For example:

```python
user = User.objects.get(id=1)
```


---

### 10. (Sibsankar Manna) — What is `on_delete=CASCADE`?

`on_delete=models.CASCADE` defines what should happen to related objects when the referenced object is deleted.

Example:

```python
class Match(models.Model):
    name = models.CharField(max_length=100)


class Delivery(models.Model):
    match = models.ForeignKey(
        Match,
        on_delete=models.CASCADE
    )
```

Suppose:

```text
Match 1
   |
   ├── Delivery 1
   ├── Delivery 2
   └── Delivery 3
```

If `Match 1` is deleted, Django will also delete its related deliveries:

```text
Match 1        → deleted
Delivery 1     → deleted
Delivery 2     → deleted
Delivery 3     → deleted
```

So `CASCADE` means:

> Delete the related objects when the referenced object is deleted.
