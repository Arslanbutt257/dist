# [PAYSOL Dashboard Django] 

## ✨ UP & Running Salvador UI
> 👉 **Step 1** Clone from github repository https://github.com/Dr-HQ/Salvador_UI.git

> 👉 **Step 2** Extract Tesseract-OCR in Salvador_UI/AI_source/sources, Place Tesseract-OCR folder in the same directory .

> 👉 **Step 3** CREATE A PYTHON ENV 
      Conda create –name env-name python=3.9.13

> 👉 **Step 4** Conda activate env-name


> 👉 **Step 5** Conda install -c conda-forge poppler

> 👉 **Step 6** Pip install –r requirements.txt

> 👉 **Step 7** python manage.py makemigrations 
                python manage.py migrate 

> 👉 **Step 8** python manage.py runserver 

## ✨ Create a new `.env` file using sample `env.sample`

The meaning of each variable can be found below: 

- `DEBUG`: if `True` the app runs in develoment mode
  - For production value `False` should be used
- `ASSETS_ROOT`: used in assets management
  - default value: `/static/assets`
- `OAuth` via Github
  - `GITHUB_ID`=<GITHUB_ID_HERE>
  - `GITHUB_SECRET`=<GITHUB_SECRET_HERE> 

<br />

### 👉 Set Up for `Unix`, `MacOS` 

> Install modules via `VENV`  

```bash
$ virtualenv env
$ source env/bin/activate
$ pip3 install -r requirements.txt
```

<br />

> Set Up Database

```bash
$ python manage.py makemigrations
$ python manage.py migrate
$ python manage.py generate-api     # optional
```

<br />

> Start the app

```bash
$ python manage.py runserver
// OR with https
$ python manage.py runsslserver 
```

At this point, the app runs at `http://127.0.0.1:8000/`. 

<br />

### 👉 Set Up for `Windows` 

> Install modules via `VENV` (windows) 

```
$ virtualenv env
$ .\env\Scripts\activate
$ pip3 install -r requirements.txt
```

<br />

> Set Up Database

```bash
$ python manage.py makemigrations
$ python manage.py migrate
$ python manage.py generate-api     # optional
```

<br />

> Start the app

```bash
$ python manage.py runserver
// OR with https
$ python manage.py runsslserver 
```

At this point, the app runs at `http://127.0.0.1:8000/`. 

<br />

## ✨ API Generator

This module helps to generate secure APIs using DRF via a simple workflow: 

- Edit/add your model in `apps/models.py`
- Migrate the database:
  - `python manage.py makemigrations apps` # this will generate the new SQL
  - `python manage.py migrate`             # this will apply the changes
- Update Configuration:
  - `core/settings.py`, section `API_GENERATOR` 
- Generate the API code:
  - `python manage.py generate-api`        # the new code is saved in `apps/api`
- Access the API in the browser:
  - `/api/MODEL_NAME/`

The API is secured using the JWT token provided by `/login/jwt/` request (username & password should be provided).  

- GET requests are public (GET all, get Item)
- Mutating requests are protected by token generated based on the user credentials (`username`, `pass`). 

> Two POSTMAN Collections are provided in the `media` directory: 

- [Books API](./media/api-books.postman_collection) - that uses PORT **5000* for the api
- [Books API 2](./media/api-books-docker.postman_collection) - that uses PORT **5085* for the api (default port in Docker)

In case both port are unusable in your environment, feel free to edit the files before POSTMAN import.

<br />

## ✨ Dynamic DataTables

This module helps to generate dynamic view for all models defined in `apps/models.py`. How to use it: 

- Edit/add your model in `apps/models.py`
- Migrate the database:
  - `python manage.py makemigrations`      # this will generate the new SQL
  - `python manage.py migrate`             # this will apply the changes
- Update Configuration:
  - `core/settings.py`, section `DYNAMIC_DATATB` 
- Access the dynamic view in the browser:
  - `/datatb/MODEL_NAME/`  

<br />

## ✨ Create Users

By default, the app redirects guest users to authenticate. In order to access the private pages, follow this set up: 

- Start the app via `flask run`
- Access the `registration` page and create a new user:
  - `http://127.0.0.1:8000/register/`
- Access the `sign in` page and authenticate
  - `http://127.0.0.1:8000/login/`

<br />

In the AI_source/source please do extract Tesseract-Ocr.zip in the same directory

## ✨ Connecting to Microsoft 365

    To get the client ID and client password in Microsoft 365, you need to create a new application in the Azure Active Directory (AAD) associated with your Microsoft 365 tenant.

    Here are the steps to create a new application in AAD and get the client ID and client password:

1.  Sign in to the Azure portal using your Microsoft 365 account.

2.  In the Azure portal, navigate to the "Azure Active Directory" section.

3.  In the "Manage" section, click on the "App registrations" option.

4.  Click on the "New registration" button.

5.  Enter a name for your application and select the supported account types.

6.  Click on the "Register" button.

7.  After the application is registered, the client ID and client secret will be displayed on the "Overview" page for the application. Make sure to copy and save these values, as you will need them later when authenticating with Microsoft 365 using the client ID and client secret.

Please note that the client secret is a sensitive value and should be treated with care. You should not share it with anyone or include it in any public code repositories.

Please refer to the Azure Active Directory documentation for more information on how to create and manage applications in AAD.

The project is coded using a simple and intuitive structure presented below:

```bash
< PROJECT ROOT >
   |-- AI_source/
   |    |--sources/
   |    |   |--Release-22.01.0-0
   |    |   |--Tesseract-OCR
   |    |   |--Supplier.xlsx
   |    |--temp/
   |    |--BST.py
   |    |--BST_Tree.py
   |    |--extraction.py                   #Holds all of the code for pdf to text and then extracting fields logic
   |    |--tokenizer.py
   |-- core/                               # Implements app configuration
   |    |-- settings.py                    # Defines Global Settings
   |    |-- wsgi.py                        # Start the app in production
   |    |-- urls.py                        # Define URLs served by all apps/nodes
   |
   |-- apps/
   |    |
   |    |-- home/                          # A simple app that serve HTML files
   |    |    |-- views.py                  # Serve HTML pages for authenticated users
   |    |    |-- urls.py                   # Define some super simple routes  
   |    |
   |    |-- authentication/                # Handles auth routes (login and register)
   |    |    |-- urls.py                   # Define authentication routes  
   |    |    |-- views.py                  # Handles login and registration  
   |    |    |-- forms.py                  # Define auth forms (login and register) 
   |    |
   |    |-- static/
   |    |    |-- <css, JS, images>         # CSS files, Javascripts files
   |    |
   |    |-- templates/                     # Templates used to render pages
   |         |-- includes/                 # HTML chunks and components
   |         |    |-- navigation.html      # Top menu component
   |         |    |-- sidebar.html         # Sidebar component
   |         |    |-- footer.html          # App Footer
   |         |    |-- scripts.html         # Scripts common to all pages
   |         |
   |         |-- layouts/                   # Master pages
   |         |    |-- base-fullscreen.html  # Used by Authentication pages
   |         |    |-- base.html             # Used by common pages
   |         |
   |         |-- accounts/                  # Authentication pages
   |         |    |-- login.html            # Login page
   |         |    |-- register.html         # Register page
   |         |
   |         |-- home/                      # UI Kit Pages
   |              |-- index.html            # Index page
   |              |-- 404-page.html         # 404 page
   |              |-- *.html                # All other pages
   |
   |-- requirements.txt                     # Development modules - SQLite storage
   |
   |-- .env                                 # Inject Configuration via Environment
   |-- manage.py                            # Start the app - Django default start script
   |
   |-- ************************************************************************
```

<br />
