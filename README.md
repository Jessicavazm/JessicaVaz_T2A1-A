# Project - workbook (t2) Part A

# Q1
The typical architecture of an API is designed to handle http requests such as get, post, patch and delete. Flask is lightweight yet powerful Python based framework that depends on Werkzeug (WSGI library), Jinja (for rendering the pages on server) and Click (for Flask commands lines and custom commands). All dependencies are installed automatically when you instal Flask. 

- The typical architecture of an API project starts with creating our directory folder, following by creating a virtual environment and activating it.

- Requirements.txt file contains required packages to connect API to database, make data available and readable between applications. Bellow is an example of a list of required packages and it's functionalities.
    - Psycopg2 = works as the driver to link flask to database.
    - Marshmallow = it helps flask to read data from/ to database.
    - Marshmallow_sqlalchemy = extension that facilitates integration between marshmallow and sqlalchemy, it generates schemas based on sqlalchemy models that is used for data serialization/deserialization.
    - Flask_bcrypt = Used for handling sensitive data and password encryption.
    - Flask_jwt_extended = Used for authentication methods, token creation. 

![Example of requirements.txt file](./screenshots/requirements.txt.png)

- Main.py 
    - This file contains the core code for the application. 
    Start from importing Flask class from flask package to create the app instance. Wrap the app definition inside of a function (this creates a application factory, allows the creation of multiple instances and configurations which is extremely useful for testing).
    Import `os` to fetch environment variables from .env file to define configurations such as URL and Secret key.
    Import objects from init.py file and initialise them passing the Flask app instance as a parameter in the init method.
    Import Blueprint from controllers folder and register them in the app to be able to use it's commands and routes.

- Init.py
    - This file contains all the classes imported from necessary packages to run the API. In this example,
    the classes imported are SQLAlchemy, Marshmallow, Bcrypt and JWTManager. It also contains the objects created from imported classes to initialise objects and use them in the main.py file. Importing the classes and initialising the objects in a different file is very beneficial, it ensures data organisation, data modularisation and code scalability.

- Models folder
    - In this folder, you can have a file for model and another file for schema (helpful in big projects for more organisation) or you can have model and the schema in one file such as in the example provided as a reference.
    - Model needs to import from init the instance from SQLAlchemy create the table and define table.
    - This file contains a class which creates a table and defines the attributes (columns values and value types), the structure is inherited from SQLALchemy. Variable __tablename__ sets the name of table in Database.
    - Schema Class is created with a marshmallow extension to serialise and deserialise data into Python readable data and vice and versa. First, the instance from marshmallow needs to be imported from init.py for this process to happen. This process ensures the request can be received by the API, and the API can send back responses to it's requests.
    - Class Meta defines what fielders will be included in serialisation/deserialisation.
    - Schemas objects are created to handle single or multiple items when performing operations on data. Exclusion of sensitive data is performed using `exclude=[]` passed in the object's parameter.

- Controllers folder
    - Blueprints are placed in each file controller files for modularisation, it makes each module independent.
    - Cli_controllers file:
        - Contains the cli_controllers file with custom commands that are created to perform operations in the database such as create, seed and drop tables. These commands can automatically insert values in database by creating instances of the model class and inserting values in the commands code (helpful for fast api testing).
        - Features:
        Create: Initializes database tables.
        Seed: Inserts initial data into the database by creating instances of model classes.
        Drop: Removes all database tables.
        - CLI commands file needs to import instance of SQLAlchemy (access database), Bcrypt (for hashing password) and Model class from models directory (creates and manages tables/objects).

    - Auth_controller:
        - Contains the authorisation file, this file contains routes for authentication such as registration, login, token creation. 
        - This file imports request from flask to handle https incoming requests, model and schema from models directory to create an instance, bcrypt for hashing password, create_access_token to create a JWT that will be returned to user when authentication is successful.
        - Timedelta is also used when creating the JWT to give the token an expiring time for security purposes.
        - Errorcodes is imported for personalised error messages in except block.
        - Register route and Login routes both uses `POST` method since both routes operates on data.
    
    #### Examples of routes in auth_controller file:
         Register route:
         Handles user registration.
         Accepts user details like name, email, and password.
         Hashes the password for security.
         Adds the user to the database and returns the user data or an error message if something goes wrong.
        
         Login route:
         Handles user login.
         Accepts email and password from the user.
         Verifies the credentials against the stored data.
         If valid, generates a JWT token that the user can use to authenticate further requests.
         Returns the token and user details or an error message if login fails.

- Gitignore
    - File contains all files that should be ignored when pushing to source control such as GIT. Files contains sensitive data or are not relevant to be pushed into the repository.
- README.md
    - File containing important and relevant information about flask app, it's purpose, setup instructions and how to use API.
- .flaskenv
    - File contains environment variables directly related to Flask. `FLASK_APP` is set here to tell our flask what name to look for to run our API. The port can also be set in this file.
- .env 
    - File contains environment variables indirectly related to Flask, as it contains sensitive information, this file is usually added on .gitignore file. This file contains URL variable which is responsible for connecting API to DATABASE, sensitive information such as database username and password is included in this variable. This file also contains a variable that stores a secret key that is used to sign and verify JWT.
- .env.example
    - This file contains variable names without the value or with 'fake' value set in .env file. This file is created to point out the necessary environment variables to run the application. 
- Tests
    - Folder contains unit tests, integration tests to test functionality of API and make sure API works as expected.

- Bellow is an example of the Trello API structure we are doing in class.
![Example of API structure](./screenshots/flaskscreens.png) 

- Example of API structure from https://flask.palletsprojects.com/
![Example of API structure from flask documentation](./screenshots/API_structure.png)

References:

Flask (2010). Welcome to Flask — Flask Documentation (3.0.x). [online] flask.palletsprojects.com. Available at: https://flask.palletsprojects.com/en/3.0.x/. 
‌
GeeksforGeeks. (2023). Flask Tutorial. [online] Available at: https://www.geeksforgeeks.org/flask-tutorial/.

# Q2 

## PostgreSQL
PostgreSQL was created back in 1986 at the University of California, Berkeley. Originally the system was named POSTGRES in relation to the Ingres database which was also developed in the same university. Later on, in 1996 the project was renamed from Postgres to PostgreSQL to reflect the support to SQL (Structure query language). The project was created under the professor Michael Stone breaker. PostgreSQL is one of the most older database systems and it's extremely popular due to it's reliability and architecture. It's an open source database system which means it's not owned by a single company or owner and source code can be accessed by anyone. The database system is managed by a group of developers and volunteers called PostgreSQL Global Development Group. 
PostgreSQL is currently on version 16, with version 16.4 released on August 8, 2024.

### Pros of PostgreSQL
- It complies with ACID (Atomicity, Consistency, Isolation and Durability) since 2001, these four pillars when applied to database guarantees the data stays consistent and preserves data integrity.
- Use of PK(Primary key), FK(Foreign key) and constraints also ensures data integrity.
- It complies with SQL standards which helps when migrating from other SQL databases.
- Flexibility: PostgreSQL can either be used as relation db system or non relational (NoSQL) for JSON data storage and query.
- DB system is compatible with most computer operating systems such as Linux, Windows, MacOS, BSD and Solaris.
- Open source and free of charge, open source brings a sense of thrust between users and developers. Since source code is open to anyone, users are able to inspect and modify the software according to their needs free of charge. Open source can be also used for learning purposes for developers to upgrade their skills by inspecting,modifying and contributing to code.
- Strong community that contributes to software development, provides support and resources. Community is very driven when it comes to report and fix bugs leading to a more improved and reliable system.
- Supports a great variety of query and procedural languages such as SQL, PL/pgSQL, Python, Perl.
- Multi-Version concurrency Control allows multiple data to be processed simultaneously without interfering with each other.
- Accepts Primitives data, Structured data such as Date/time, Arrays, Range, JSON, JSONB, XML, Geometry Data and it also allows you to custom your own data(composite and custom types).
- PostgreSQL supports video, audio, and image files.
- Allows functions customizations that are useful for performing calculations or simplifying queries.
- Indexing and Advanced Indexing improves database query performance by quicker way to access values.
- Table partitioning which is helpful when it comes to table management and readability, this function slipt larger table in smaller tables but the table is still managed as one piece.  
- Incorporates Write-Ahead Logging (WAL) which is a feature that ensures data integrity by recording changes to database first in a log before the actual database, so in case of a failure, it's possible to recover the database to it's previous state.
- Robust Access-Control System which allows the owner of the table to grant and revoke permissions to other users making data more secure. Column and row level security specifies what columns or rows users are allowed to view and perform modifications.
- PostgreSQL supports many different types of authentication such as GSSAPI, SSPI, LDAP, SCRAM-SHA-256 and Certificate. Pgcrypto extension can also be used in PostgreSQL to perform hashing and encryption to handle sensitive data and ensure data security.
- Suitable for cloud environments.

### Cons of PostgreSQL
It appears that PostgreSQL has relatively few downsides. Here are some potential drawbacks I’ve found:
- Since PostgreSQL is an open source and not owned by a particular organisation, the database software does not carry liability for damages or offers warranty of any kind.
- Due to it's vast number of functionalities which is also considered a strong feature, it can be intimidating to users who are new to the system or users who don't have much experience with relational databases systems.
- Data migrating/ and software updates can be complex/slow. 
- Performance can be considered slower than SQL Server and MySQL.

References: 

PostgreSQL (2019). PostgreSQL: About. [online] Postgresql.org. Available at: https://www.postgresql.org/about/.

Amazon Web Services (n.d.). What is PostgreSQL? – Amazon Web Services. [online] Amazon Web Services, Inc. Available at: https://aws.amazon.com/rds/postgresql/what-is-postgresql/. 

Dhruv, S. (2019). Pros and Cons of using PostgreSQL for Application Development. [online] Aalpha. Available at: https://www.aalpha.net/blog/pros-and-cons-of-using-postgresql-for-application-development/. 

Dhruv, S. (2019). Pros and Cons of using PostgreSQL for Application Development. [online] Aalpha. Available at: https://www.aalpha.net/blog/pros-and-cons-of-using-postgresql-for-application-development/. 

# Q3 - mark 6
Discuss an implementation of an Agile project management methodology for an API project.

Agile Kanban



# Q4 
Source Control is a crucial aspect of the API development process, offering numerous benefits. It helps track changes made to application, facilitates collaboration among developers and ensures smooth deployment. One of the most popular source control system is GIT, it's free and open source. Git can be used from small to bigger projects. The example I'm going to give uses git for the control system. 
Some of the benefits of source control include:
- All changes to code are tracked including edition, deletion and branch merging. The tracking history also includes who performed the change, day/ time and comments about why change has been performed. Track history is very important because when application needs to be improved or bugs need to be fixed, developers can refer back to track history which allows them improve application faster.
- Branches is another powerful feature that allows developers to work on features independently without conflicting with other branches. Once all changes has been made, testing has been done and application is working as expect, developers can merge branches and delete the extra branches once they have been merged into the main branch (this step is optional). 
- Branches can be used for trying out ideas, testing. Some companies prefer the idea of creating a branch for each feature of the application but there's plenty of other workflow options to choose from when working with source control.

### Process of a source control for API:
- Create a project directory, create and activate Virtual environment, install required packages to build application and freeze them into requirements.txt file.
- Create a git repository for your repository and add README.md file.
- Create a .gitignore file in the application folder to mention all files git should ignore when pushing to repository, this folder usually includes __pycache__, virtual environment, environment variable (sensitive information).
- Create a init file to initialise things and main.py file which will contain the core code.
- Create environment variables to handle sensitive information, import variables in the main and init files. Add this file to .gitignore
- Create environment variables examples or sample files to tell other developers there's env variables in the project and they need to set them on their end.
- After creating all the necessary and main files for the application perform add . and push everything to main branch.
- Create a new folder/ files to create and define models, schemas and controllers to work on app features.
- Create a new branch that will handle features of the application such as authentication. The convention name for branches starts with the name feature, eg: feature/authentication, this indicates this branch works on specific feature.
It's a good idea to create a branch for each feature as it modularise the code even more.
- Make sure you are in the feature branch created, add, commit and push changes with meaningful messages as usual. First time you push code to new branch you will have to mention the branch name eg: git push -u branch_name 
- Always perform git status to be aware of modified files that hasn't been pushed into repository yet.
- Once application is working as expected and all testing has been done, perform pull request (this method merges the extra branches to the main branch).
- Compare and review codes in both branches and make sure there's no conflict. In case of a branch conflict, you need to git pull first, solve the conflict and then create pull request again.
- When there's no conflict and you are able to merge branches you will get a green light in the pull request window. In this window, you can add branch description, labels, reviewers and assignees (these are optional).
- After filling the information you can create the pull request, in the following page you will have information about commits performed in this branch, see changes performed in files, see conversation between colleagues, add rules required before merging branches and add comments or reviews.
- Once all requirements has been achieved and app is working as it should you can merge the pull request and confirm the merge.
- Once branch is merged, you will see an acknowledgement confirmation. There's an option to safely delete the branch or you can keep it.
- After pull request has been performed, you can see all the files under main branch.
- Back in VS Code, you'll need to run git pull to retrieve and view the latest changes from the remote repository.

#### Screenshots of source control process
![Example of trello source control](./screenshots/git1.png)
![Example of source control merge](./screenshots/merge_eg.png)

References: 

Git (2019). About - Git. [online] Git-scm.com. Available at: https://git-scm.com/about.

Atlassian (2019). What is version control. [online] Atlassian. Available at: https://www.atlassian.com/git/tutorials/what-is-version-control.
‌
Atlassian (n.d.). Git Merge | Atlassian Git Tutorial. [online] Atlassian. Available at: https://www.atlassian.com/git/tutorials/using-branches/git-merge.

‌
# Q5 
API testing can be performed using testing tools such as Insomnia, Postman, SoapUI. Insomnia is the API we have been using in our API testing. Insonmia performs unit tests made by HTTP requests and it depends Mocha framework and Chai for assertions. Insomnia also supports authentication testing and another important aspect about this type of testing is the developer needs to know the expected outcome in order to determine API's efficiency. 
There are few different types of HTTPS requests:
- GET = Fetches data from resource
- POST = Send data to the server to create or update a resource
- PUT = Overwrites the whole resource
- PATCH = Updates specific patch in the resource
- DELETE = Delete the resource
- HEAD = Only fetch the data from the headers(meta-data)
- OPTIONS = Describes communications available
- CUSTOM: Available to create a custom request

#### Steps on how to perform API testing with Insomnia, testing authentication.

- Perform `flask run` in API on terminal
- In Insomnia dashboard create a new folder, and click on HTTP request
- Choose the type of request, example: POST request
- Write down URL, in our example we are using local host and port: 8080 we set in .flaskenv file.
    localhost:8080/auth/login
- In the request body, choose JSON type and write credentials.
- After sending the request, on the right hand side you can see if your request has been successful or not. This part contains response code, time that request took to be performed and file size. You can also see how the response looks like in preview, see header info (meta-data), cookies, console and mock.
- In case request is successful and credentials match, a JWT will be created and returned back in the response body to user. 
- In case request is not successful, Insomnia displays an error message, error code and trace back to help developers fixing the bug.
- To send authentication in the `post` request, click on `auth` tab, choose the type of authentication you want, and then paste auth code in the request body. Insomnia supports different types of auth including: Bearer Token (the one we have been using), Basic Auth, Digest Auth, OAuth 1.0, OAuth 2.0 and more.

#### Common error codes
    400 Bad Request: The request was malformed or invalid.
    401 Unauthorized: Authentication is required and has failed or not been provided.
    403 Forbidden: The server understood the request but refuses to authorize it.
    404 Not Found: The requested resource could not be found.
    500 Internal Server Error

#### Examples of testing cases for error handling in login route and authentication route from Trello API.
![Example of registration testing](./screenshots/Insomnia1.png)
![Example of authentication testing](./screenshots/Insomnia2.png)

References:
Coder Academy APR-STD Trello_API 

Insomnia.rest. (2021). Unit Testing | Insomnia Docs. [online] Available at: https://docs.insomnia.rest/insomnia/unit-testing [Accessed 22 Aug. 2024].

‌
# Q6 
CIA triad is an Information system security model that has 3 core principles: Confidentiality, Integrity and Availability. This model is widely used by organisations and it's main purpose is to keep data secure. The three components corelate to each other.

- Confidentiality: 

It ensures data is only accessible to view and edit to authorised users by implementing control's measures such as authentication, encryption and data masking. Authentication method ensures user's identification, it can be done through username and password, tokens, biometric identifiers such as fingerprint or facial and plenty more. Encryption methods ensures data is secured in the transit process by making it unreadable. When you encrypt a file, it generates a key which is only granted to authorised users. With the correct key, users are able to perform further operation which requires authentication before hand. Masking is another method that involves replacing the original data with a fictional data. Monitoring data is another crucial process in the confidentiality method. Organisations can use applications such as Intrusion detection system (IDS) and Intrusion prevention system (IPS) to prevent and report any malicious activity. Another powerful tool is to report security incidents, this can also help to identify any security breach that might occur in the future. For this reason, employees should be trained on the types of security breaches and best practices so they can identify potential problems in the future and understand how to handle data securely.

- Integrity: 

This component is responsible for data's integrity during transit or rest processes. Some techniques to help with integrity are checksum and hash functions. Checksum is unique value that is generated after processing the original data, in case of an accidental error, a different checksum will be generated indicating the data has been altered. Hash function converts a file to fixed strings of bytes(Hexadecimal). Like Checksum, the Hash function produces a unique value that is used to check if data has been modified.<br>
Version control system such as GIT is also used as a method to ensure data integrity, allowing users to track all changes and restore previous version if needed.
System and data redundancy are another important measures organisations can use to make sure their data is complete and operations can be maintain in case of failure/loss. Often backups and multiple copies in different systems or locations can also be beneficial to ensure if their suffer an cyber attack they don't have a total loss of data.

- Availability:

This component ensures the data is available all the time to authorised users for viewing and modifications when it needed. To ensure maximum availability, the system must be safe from malicious activities and data should be stored/managed safely. This component goes side by side with confidentiality and integrity components. Some measures to make this happen includes conducting regular system maintenance updates, implements measures to protect against malicious attacks, make use of data and system redundancy, have a recovery plan, use of Load balancers to distribute incoming traffic across multiple servers and preventing one server to become overwhelmed resulting in better performance. Load balance softwares includes HAProxy and NGINX or Cloud-based includes AWS Elastic and Azure. Recover plans can include risk assessments to identify threats and potential risks, and recovery procedures to indicate what steps to take in case of data/ system disruption.

References:

Infosecurityeurope.com. (2024). What are the 3 principles of Information Security? [online] Available at: https://www.infosecurityeurope.com/en-gb/blog/guides-checklists/principles-of-information-security.html.

Hashemi-Pour, C. (2023). What is the CIA Triad? Definition, Explanation and Examples. [online] TechTarget. Available at: https://www.techtarget.com/whatis/definition/Confidentiality-integrity-and-availability-CIA.


# Q7 - mark 12
To implement the component `Confidentiality` in an API, we can use create an authorization controller which will handle user's authentication, make use of Bcrypt to store hashed passwords in tables and environment variables to handle sensitive information from JWT and Database URL.
When it comes to database, it's important to exclude sensitive info when retrieving fields in Schemas. This can be done by passing exclude in the Schemas instances.
    
    class UserSchema(ma.Schema):
        class Meta:
            #Fields
            fields = ("id", "name", "email", "password", "is_admin")

    
    user_schema = UserSchema(exclude=["password"])
     
    users_schema = UserSchema(many=True, exclude=["password"])


- Example of B.crypt being used to hash user's password and how the hashed password looks like in a DB.

User(
            email = "admin@email.com",
            password = bcrypt.generate_password_hash("123456").decode("utf-8"),
            is_admin = True
)

![Example of Postgresql](./screenshots/postgresql.png)


Example of an auth controller routes that register and authenticate users. For this example, JWTManager and Bcrypt packages needs to be imported to hash password and create JWT. <br>
Important steps for registering User:
- Request is used to retrieve information from data body
- Create an instance of the User model, fetch fields and store data in User object.
- Hash password and store it in a variable, import Bcrypt from init file to execute this.
- Add and commit to DB
- Return acknowledgment message

Important steps for authenticating user:
- Fetch data from request body.
- Create a stmt to find User with provided email and password and execute stmt.
- If user exist, check_password_hash method checks hash value from request body against stored hash in database.
- If everything matches, use create_access_token method to create a JWT and give it an identity, in this example user id is used. Convert to string since identity only accept string values.
- Use timedelta method to set an expiring time for security purposes.
- Return an acknowledgment message back to user with user information such as email and token.
- Token can be requested for further operations such as edit or delete tables.

![Example of Register route](./screenshots/auth2.png)

![Example of Login route](./screenshots/auth_example.png)


Another example of confidentiality is to use environment variables such as `.env` to handle sensitive information when creating API and connecting API to database. Environment variables can be called in the main.py and should be excluded of the source control. In this example, .env stores sensitive URL DB info and JWT secret key. To tell other developers about existing variables, we can create an example or sample of environment variables. To fetch these variables in main.py, we need to import OS.

Example of .env file
    DATABASE_URL = postgresql+psycopg2://trello_dev:123456@localhost:5432/trello_db
    JWT_SECRET_KEY = "secret"

Example of .env.example or sample
    DATABASE_URL =
    JWT_SECRET_KEY = 
    
In main.py file we can call the env variables with the help of the OS method, this method allows us to fetch those variables from the .env file = `os.environ.get("variable_name)`:

![Example of environment variables](./screenshots/env_variables.png)

References:
Week 4 and 5 Trello API Zoom classes

# Q8 - mark 12 (second main question)
Explain the legal obligations that developers of a social media website or social media application would have in regards to handling user data, with reference to any applicable laws or acts.


REF:
https://developer.atlassian.com/platform/marketplace/data-privacy-guidelines/
# Q9 - mark 6
Describe the structural aspects of the relational database model. Your description should include information about the structure in which data is stored and how relations are represented in that structure.



# Q10 - mark 6
Describe the integrity aspects of the relational database model. Your description should include information about the types of data integrity and how they can be enforced in a relational database.


# Q11 - mark 6
Describe the manipulative aspects of the relational database model. Your description should include information about the ways in which data is manipulated (added, removed, changed, and retrieved) in a relational database.



# Q12 - mark 42 (main question)
Conduct research into a web application (app) and answer each of the following sub-questions:

List and describe the software (tech stack) used by the app. 

Describe or make educated guesses about the hardware used to host the app.

Describe the interaction of technologies within the app.

Describe the way data is structured within the app’s database(s).

Identify the entities/tables that are tracked within the app’s database(s).

Identify the relationships and associations between the entities/tables identified in sub-question E.

Design an entity relationship diagram (ERD) based on the answers provided to sub-questions E and F. This must represent a relational database model, even if the app itself uses something other than a relational database model.


