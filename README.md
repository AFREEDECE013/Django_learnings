# Django_learnings

What is Django?
“Django is a high-level Python web framework used to build web applications and backend APIs quickly and securely.”

It provides built-in features like:
- ORM for database operations
- Authentication and authorization
- URL routing
- Admin panel
- Middleware
- Security features
Interview answer:
“Django is a Python web framework that follows the MVT architecture and provides many built-in features, which helps developers build scalable and secure web applications faster.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Django Architecture
Django follows the MVT (Model–View–Template) architecture.
- Model → Handles database and data structure.
- View → Contains business logic and handles requests/responses.
- Template → Handles the presentation/UI layer.
Flow:
Client → URL → View → Model → Database → View → Template → Response
Interview answer:
“Django follows the MVT architecture. The Model manages data, the View handles business logic and requests, and the Template is responsible for presentation. URLs route incoming requests to the appropriate view.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Django Models
“A Django Model is a Python class that represents a database table. It defines the fields, data types, and relationships between data.”

Example:
class User(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField(unique=True)

Here, Django creates a database table with name and email fields.
Interview answer:
“Models define the structure of our database and allow us to interact with the database using Django ORM instead of writing SQL for every operation.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Views / DRF Views
Django View:
“A view handles an HTTP request, performs the required business logic, and returns an HTTP response.”

Example:
def get_users(request):
    users = User.objects.all()
    return JsonResponse({"users": list(users.values())})

DRF View:
“Django REST Framework views are used to build APIs. They provide features for handling HTTP methods like GET, POST, PUT, and DELETE.”

Common DRF views:
- APIView
- GenericAPIView
- ViewSet
Interview answer:
“In Django, views handle requests and responses. In DRF, views are specifically designed for APIs and make it easier to handle HTTP methods, serialization, authentication, and permissions.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Serializers in DRF
“A serializer converts complex data like Django model objects into JSON so it can be sent through an API. It also converts incoming JSON into Python data and validates it.”

Example:
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = ["id", "name", "email"]

Interview answer:
“Serializers are mainly used for data conversion and validation in Django REST Framework. They convert model objects to JSON for responses and validate incoming request data.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

URLs in Django
“Django URLs are used for mapping incoming HTTP requests to the appropriate view.”

Example:
urlpatterns = [
    path("users/", views.get_users),
    path("users/<int:id>/", views.get_user),
]

Here:
- /users/ → calls get_users
- /users/5/ → calls get_user with id=5
Interview answer:
“The URL configuration acts as a routing layer. It matches the requested URL and HTTP method pattern to the appropriate Django or DRF view.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Database in Django
“Django provides an ORM (Object-Relational Mapper) that allows us to interact with the database using Python objects instead of writing SQL directly.”

For example:
users = User.objects.filter(is_active=True)

Django supports databases like PostgreSQL, MySQL, SQLite, and Oracle.
Interview answer:
“In Django, we usually interact with the database through Django ORM. Models represent tables, and the ORM handles queries, relationships, and database operations. Django migrations are used to apply model changes to the database.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Django Project vs App
Django Project
“The project is the complete Django application. It contains the main configuration, settings, URL configuration, and deployment setup.”

Django App
“An app is a specific module or feature inside the project, such as users, payments, or products.”

Example:
my_project/
├── settings.py
├── urls.py
│
├── users/
├── payments/
└── products/
Interview answer:
“A Django project is the overall application, while a Django app is a reusable module that handles a specific functionality within that project.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Django Models
“A Django Model is a Python class that represents a database table. It defines fields, data types, and relationships.”

Example:
class User(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField(unique=True)

Django ORM lets us query it without writing SQL directly:
users = User.objects.all()

Interview answer:
“Models define the database structure in Django. Django ORM uses these models to perform database operations like create, read, update, and delete.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Django Migrations
“Migrations are used to track and apply changes made to Django models to the database schema.”

For example, if I add a new field to a model:
class User(models.Model):
    name = models.CharField(max_length=100)
    age = models.IntegerField()  # New field

I run:
python manage.py makemigrations
python manage.py migrate
- makemigrations → Creates migration files based on model changes.
- migrate → Applies those changes to the database.
Interview answer:
“Migrations act like version control for the database schema. They help us safely track and apply model changes to the database.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Django ORM
“ORM stands for Object-Relational Mapping. Django ORM allows us to interact with the database using Python code instead of writing SQL queries directly.”

Example:
# Get all users
users = User.objects.all()

# Filter users
users = User.objects.filter(age__gte=25)

# Create a user
User.objects.create(name="Ahmed", age=25)

Interview answer:
“Django ORM maps Python models to database tables and provides methods like filter(), get(), create(), and update() to perform database operations.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

QuerySets
“A QuerySet is a collection of database queries or objects returned by the Django ORM. It allows us to retrieve, filter, and manipulate database records.”

Example:
users = User.objects.filter(age__gte=25)

Here, users is a QuerySet.
Common methods:
- filter() → filter records
- get() → get a single record
- all() → get all records
- exclude() → exclude records
- order_by() → sort records
Important: QuerySets are lazy, meaning the database query is usually executed only when the results are actually needed.
Interview answer:
“A QuerySet represents a collection of database records and provides methods to query them. Django QuerySets are lazy, so the database isn't hit until the QuerySet is evaluated.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

select_related()
“select_related() is used to optimize database queries by fetching related objects using a SQL JOIN in a single query.”

Example:
orders = Order.objects.select_related("customer").all()

Without select_related(), accessing each order's customer may cause additional database queries.
With it, Django fetches the Order and Customer together.
Interview answer:
“I use select_related() for ForeignKey and OneToOne relationships to avoid unnecessary database queries and reduce the N+1 query problem.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

prefetch_related()
“prefetch_related() is used to optimize queries for related objects, especially Many-to-Many and reverse ForeignKey relationships.”

Example:
orders = Order.objects.prefetch_related("items").all()

Django fetches the orders and their items using separate queries and combines them in Python.
select_related() vs prefetch_related()
- select_related() → SQL JOIN, mainly ForeignKey / OneToOne
- prefetch_related() → separate queries, mainly Many-to-Many / reverse ForeignKey
Interview answer:
“Both are used to avoid N+1 queries. select_related uses a SQL join for single-valued relationships, while prefetch_related uses separate queries for multi-valued relationships.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Django REST Framework (DRF)
“Django REST Framework is a toolkit built on top of Django for building RESTful APIs.”

It provides:
- Serializers → data conversion & validation
- API Views / ViewSets → handle API requests
- Authentication & Permissions
- Pagination
- Throttling
- Browsable API
Interview answer:
“DRF makes it easier to build APIs with Django by providing serializers, API views, authentication, permissions, pagination, and other features required for REST APIs.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Serializers in DRF
“Serializers are used to convert complex Python or Django model objects into JSON for API responses, and convert incoming JSON into validated Python data.”

Example:
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = ["id", "name", "email"]

Interview answer:
“Serializers handle serialization, deserialization, and validation in DRF. They convert model data to JSON and validate incoming request data before saving it.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

ViewSets in DRF
“A ViewSet groups related API operations for a model into a single class, instead of creating separate views for each operation.”

Example:
from rest_framework.viewsets import ModelViewSet

class UserViewSet(ModelViewSet):
    queryset = User.objects.all()
    serializer_class = UserSerializer

ModelViewSet provides common operations like:
- GET → list/retrieve
- POST → create
- PUT/PATCH → update
- DELETE → delete
Interview answer:
“ViewSets reduce repetitive code by grouping CRUD operations for a resource in one class. They are commonly used with DRF routers to automatically generate API URLs.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Authentication in DRF
“Authentication is the process of identifying who the user is before allowing access to an API.”

Common methods in DRF:
- Session Authentication → commonly used with Django sessions.
- Token Authentication → client sends an API token.
- JWT Authentication → client sends a signed token with each request.
- OAuth2 → commonly used when authentication involves an external identity provider.
Interview answer:
“Authentication verifies the identity of the user. In DRF, we can use session, token, JWT, or OAuth2-based authentication depending on the application requirements.”

Remember:
Authentication = Who are you?
Authorization = What are you allowed to do?

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Permissions in DRF
“Permissions determine whether an authenticated user is allowed to access a particular API or perform a specific action.”

Example:
from rest_framework.permissions import IsAuthenticated

class UserViewSet(ModelViewSet):
    permission_classes = [IsAuthenticated]

Only authenticated users can access this API.
Common permissions:
- AllowAny
- IsAuthenticated
- IsAdminUser
- IsAuthenticatedOrReadOnly
Interview answer:
“Authentication identifies the user, while permissions decide what that user is allowed to access or do.”

Simple example:  
“A normal user can view their profile, but only an admin can delete users.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Middleware in Django
“Middleware is a layer that sits between the client request and Django's view. It can process requests before they reach the view and responses before they are sent back.”

Common uses:
- Authentication
- Logging
- Security
- CORS
- Request/response processing
Flow:
Request → Middleware → View → Middleware → Response
Interview answer:
“Middleware is used for processing requests and responses globally. For example, authentication middleware can identify the user before the request reaches the view.”

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Django Signals
“Django signals allow different parts of an application to react to certain events without directly coupling the code.”

For example, after a user is created, we can automatically create a profile.
@receiver(post_save, sender=User)
def create_profile(sender, instance, created, **kwargs):
    if created:
        Profile.objects.create(user=instance)

Common signals:
- pre_save
- post_save
- pre_delete
- post_delete
Interview answer:
“Signals are useful when we want to automatically trigger some action when an event occurs, such as creating a profile after a user is created.”

Simple example:
User created → post_save signal → Profile created

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
