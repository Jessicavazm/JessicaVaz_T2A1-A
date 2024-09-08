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

![Example of requirements.txt file](./screenshots/requirements.png)

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
    - This file contains a class which creates a table and defines the attributes (columns values and value types), the structure is inherited from SQLALchemy. Variable tablename sets the name of table in Database.
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
PostgreSQL was created back in 1986 at the University of California, Berkeley. Originally the system was named POSTGRES in relation to the Ingres database which was also developed in the same university. Later on, in 1996 the project was renamed from Postgres to PostgreSQL to reflect the support to SQL (Structure query language). The project was created under the professor Michael Stone breaker. 

PostgreSQL is one of the most older database systems and it's extremely popular due to it's reliability and architecture. It's an open source database system which means it's not owned by a single company or owner and source code can be accessed by anyone. The database system is managed by a group of developers and volunteers called PostgreSQL Global Development Group. 

PostgreSQL is currently on version 16, with version 16.4 released on August 8, 2024.

#### Pros of PostgreSQL
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

#### Cons of PostgreSQL
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


# Q3 

Agile methodology involves going back to goals and reviewing them to keep improving. Agile breaks down a big project into smaller parts so developers can work in these smaller parts with ease.

In the Trello API, Agile can help organise and manage the creation of foundational files needed to link the API to the database, as well as to set up models, schemas, routes, and controllers.

Ways to implement agile into `Trello API` project:

### User Stories 

User stories are used to tell the developers what problem you are trying to solve and what requirements you product needs. Bellow is an user stories example for the Trello API we have building in class.

- As a customer, I want to be able to create cards, so I won't need to memorize important information.
- As a customer, I want have my cards saved, so the next time I won't need to rewrite then again.
- As a customer, I want to a function where time and date is added to card, so I can add those functions to my cards.
- As a customer, I would like to delete cards that are no longer needed, so I won't be confused.
- As a customer, I want to move cards between priority lists, so I know what I need to focus first.
- As a customer, I would like to add comments to cards, so I can directly provide updates on cards.

### Kanban

Kanban is a visual tool that allows everybody to see all tasks and how they are progressing. Kanban is usually revisited towards the end of certain phrases or sprits. In our Trello API, Kanban could be visited after completing each controller or models/schemas. Bellow is an example I have created for the Trello API.

![Example of Kanban tool](./screenshots/Kanban.png)

### Sprints, Sprint Retrospectives and Task Prioritisation

Sprints have defined properties such as task duration, `To do` and `In progress` lists, and the task's ownership.
- Create initial APP files, install required packages, set environment variables and connect API to Database, duration: 3 days, ownership: Jessica
- Create Trello's ER Diagram, duration: 1 week, ownership: Aamod
- Create Models and Schemas, duration: 2 weeks, ownership: Yrina
- Create Controllers and Routes, duration: 2 weeks, ownership: Alex
- Run unit tests on Insomnia, duration: 3 days, ownership: Jessica

Sprints retrospectives is also a powerful tool to check with the team and see the project's progress. This method helps the team to understand what has been successful, what areas needs improvement and what areas will be prioritized in the next sprint.
- Initial files has been created and DB connects to API without any issues
- CLI controller has been performing commands well 
- Auth Controller needs attention in regards to error handling
- Auth Controllers will be prioritized in the next spring

Task prioritisation defines what task comes first and what are dependent-tasks, levels of priorities and required hours for task development. Example of Trello Task prioritisation:
- High priority: 
    Initial files: APP directory, virtual environment, required packages , main.py, init file and env variables 
- High priority:
    Create models and Schemas
- High Priority: 
    Create Controllers and routes
- High Priority:
    Insomnia Tests
- High Priority:
    Git commits and pushes

References: 
TRELLO API project we are currently working on, and from `Intro to Agile` T1W2 material from ED.

# Q4 
Source Control is a crucial aspect of the API development process, offering numerous benefits. It helps track changes made to application, facilitates collaboration among developers and ensures smooth deployment. 

One of the most popular source control system is GIT, it's free and open source. Git can be used from small to bigger projects. The example I'm going to give uses git for the control system. 

Some of the benefits of source control include:
- All changes to code are tracked including edition, deletion and branch merging. The tracking history also includes who performed the change, day/ time and comments about why change has been performed. Track history is very important because when application needs to be improved or bugs need to be fixed, developers can refer back to track history which allows them improve application faster.
- Branches is another powerful feature that allows developers to work on features independently without conflicting with other branches. Once all changes has been made, testing has been done and application is working as expect, developers can merge branches and delete the extra branches once they have been merged into the main branch (this step is optional). 
- Branches can be used for trying out ideas, testing. Some companies prefer the idea of creating a branch for each feature of the application but there's plenty of other workflow options to choose from when working with source control.

### Process of a source control for API:
- Create a project directory, create and activate Virtual environment, install required packages to build application and freeze them into requirements.txt file.
- Create a git repository for your repository and add README.md file.
- Create a .gitignore file in the application folder to mention all files git should ignore when pushing to repository, this folder usually includes pycache, virtual environment, environment variable (sensitive information).
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

#### Confidentiality: 

It ensures data is only accessible to view and edit to authorised users by implementing control's measures such as authentication, encryption and data masking. Authentication method ensures user's identification, it can be done through username and password, tokens, biometric identifiers such as fingerprint or facial and plenty more. 

Encryption methods ensures data is secured in the transit process by making it unreadable. When you encrypt a file, it generates a key which is only granted to authorised users. With the correct key, users are able to perform further operation which requires authentication before hand. Masking is another method that involves replacing the original data with a fictional data. Monitoring data is another crucial process in the confidentiality method. 

Organisations can use applications such as Intrusion detection system (IDS) and Intrusion prevention system (IPS) to prevent and report any malicious activity. Another powerful tool is to report security incidents, this can also help to identify any security breach that might occur in the future. For this reason, employees should be trained on the types of security breaches and best practices so they can identify potential problems in the future and understand how to handle data securely.

#### Integrity: 

This component is responsible for data's integrity during transit or rest processes. Some techniques to help with integrity are checksum and hash functions. Checksum is unique value that is generated after processing the original data, in case of an accidental error, a different checksum will be generated indicating the data has been altered. Hash function converts a file to fixed strings of bytes(Hexadecimal). Like Checksum, the Hash function produces a unique value that is used to check if data has been modified.

Version control system such as GIT is also used as a method to ensure data integrity, allowing users to track all changes and restore previous version if needed.

System and data redundancy are another important measures organisations can use to make sure their data is complete and operations can be maintain in case of failure/loss. Often backups and multiple copies in different systems or locations can also be beneficial to ensure if their suffer an cyber attack they don't have a total loss of data.

#### Availability:

This component ensures the data is available all the time to authorised users for viewing and modifications when it needed. To ensure maximum availability, the system must be safe from malicious activities and data should be stored/managed safely. 

Availability component goes side by side with confidentiality and integrity components. Some measures to make this happen includes conducting regular system maintenance updates, implements measures to protect against malicious attacks, make use of data and system redundancy, have a recovery plan, use of Load balancers to distribute incoming traffic across multiple servers and preventing one server to become overwhelmed resulting in better performance. 

Load balance softwares includes HAProxy and NGINX or Cloud-based includes AWS Elastic and Azure. Recover plans can include risk assessments to identify threats and potential risks, and recovery procedures to indicate what steps to take in case of data/ system disruption.

References:

Infosecurityeurope.com. (2024). What are the 3 principles of Information Security? [online] Available at: https://www.infosecurityeurope.com/en-gb/blog/guides-checklists/principles-of-information-security.html.

Hashemi-Pour, C. (2023). What is the CIA Triad? Definition, Explanation and Examples. [online] TechTarget. Available at: https://www.techtarget.com/whatis/definition/Confidentiality-integrity-and-availability-CIA.


# Q7
To implement the component `Confidentiality` in an API, we can use create an authorization controller which will handle user's authentication, make use of Bcrypt to store hashed passwords in tables and environment variables to handle sensitive information from JWT and Database URL.

When it comes to database, it's important to exclude sensitive info when retrieving fields in Schemas. This can be done by passing exclude in the Schemas instances.
    
    class UserSchema(ma.Schema):
        class Meta:
            fields = ("id", "name", "email", "password", "is_admin")
        
    user_schema = UserSchema(exclude=["password"])
        
    users_schema = UserSchema(many=True, exclude=["password"])


Example of B.crypt being used to hash user's password and how the hashed password looks like in a DB.

    User(
            email = "admin@email.com",
            password = bcrypt.generate_password_hash("123456").decode("utf-8"),
            is_admin = True
        )

![Example of Postgresql](./screenshots/postgresql.png)

Example of an auth controller routes that register and authenticate users. For this example, JWTManager and Bcrypt packages needs to be imported to hash password and create JWT. 

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

Another example of confidentiality is to use environment variables such as `.env` to handle sensitive information when creating API and connecting API to database. Environment variables can be called in the main.py file and should be excluded of the source control. 

In this example, .env stores sensitive URL DB info and JWT secret key. To tell other developers about existing variables, we can create an example or sample of environment variables. To fetch these variables in main.py, we need to import OS.

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


# Q8 

Developers should be aware and comply with legal obligations when handling user's data. There are acts and obligations in place to ensure individuals information is being held safely and secured. Acts might be different from country to country however they enforce the same thing: data security. Being aware of obligations helps developers understand the responsibilities they have towards the individuals and avoid any possible legal action or penalty. They are required to implement and enforce security in their applications, ensure user acknowledgment when requesting data and clear information on how data will be used.

Developers should regularly check and update their applications to make sure they follow legal rules. They are also required to notify users if there's a data breach, such as misuse or a leak of personal information.

<b>Practices developers can follow to ensure they are complying with legal obligations:</b>

- Be aware of legal actions in place to ensure compliance.
- Ensure data security by adding extra layers of protection to the application, such as encryption, authentication, and validation.
- Obtain users consent and display clear disclosure on how data will be used.
- Offer users a clear and easy to find function to unsubscribe.
- Only collect necessary data, and remove data once it's no needed.
- Offer users the right to access, update or delete their own personal data.
- Ensure systems complies with legal obligations.
- In case of using any third party tool, ensure it also complies with legal obligations.


## Legal acts in Australia developers should be aware of.

<b>The Australian Privacy Principles(APPs) - Privacy Act 1988 </b>

Privacy Act was created on 14/12/1988 in Australia. It became effective in 1989 to protect individuals and dictate how their personal data are processed by Australia government agencies and private organisations with a turnover of $3 million or more (there is some exceptions for smaller organisations). Privacy Act is the main legislation in Australia for data protection and it gives the individuals the right to know when their data is being collected, who will have access to it and how it will be used.

Privacy act consists of 13 principles that APP entities should follow when handling personal data. It ensure entities handles data safely and only collect necessary data. The 13 principles also outline what entities need to do before sharing data across borders, how to handle unsolicited data, and the conditions for using data for marketing. They also detail steps to protect data from misuse, loss, or cyber attacks. Additionally, the principles cover obligations towards individuals, such as notifying them about data collection, allowing data corrections, keeping records of data access requests, and destroying data when it’s no longer needed or the purpose has been fulfilled.

Personal information and sensitive information can include: name, phone number, dob, biometrics, IP addresses, credit information, employment records, photos,location, criminal and health records, sexual orientation, political associations, religious beliefs, ethnic origin. Privacy Act does not cover anyone who has been deceased. The right to privacy is not absolute, which means other concerns are also taken into consideration, these concerns comes into consideration when safety and justice matters are involved. 

Under this act, individuals can choose to not disclose personal information, have access to their personal information (health, credit records), have the right to decide if they wish to not receive marketing. Individuals also have the right to make complaints about organisations regulated under Privacy Act in case the individual believes their data has been mishandled and the company has breached the security responsibilities they have towards individuals. 

Breaching the Privacy Act can result in severe penalties including civil penalty up to $2,500,000 for an individual or up to $50,000,000 for an organisation. These are the maximum penalty for serious offenses and they are described in Privacy Act section 13G. Affected individuals have the right to sue individual/ organisations for compensation.


<b>Companies under Privacy Act 1998:</b>

- Australian Government 
- Norfolk Island administration
- Organisations (individual, body corporate, partnership, unincorporated association, trust) with annual turnover of $3 million or more.
- Small business (annual turnover of $3 million or less) including: 
    - Private health service provider including gym, childcare, physiotherapy clinic, medical practitioner
    - Employee registered under Fair Work
    - Business registered with Consumer data right
    - Business listed under Privacy Regulation 2013
    - Contracted service provider for Australian government 
    - Credit reporting business
    - Business that sells/ purchase personal information


<b>Spam Act 2003 </b>

Spam ACT 2003 was created in December 2003 in Australia and enforced by Australian Communications Authority, however in 2005 it became the Australian Communications and Media Authority. The act regulates commercial electronic mails and it aims to reduce the amount of unsolicited messages sent in Australia. 

Developers are crucial when it comes to the CAN-SPAM Act of 2003 because they create and manage systems for sending marketing emails. This law requires emails to have clear opt-out options, accurate sender information, and proper consent from users. Developers need to build features into their systems to make sure users can easily unsubscribe and that all email practices follow these rules. By doing this, they help companies avoid fines and ensure their email communications follows the legal obligations.

Failing to comply with legal obligations can result in civil penalties and injunctions. Penalties depends on breach severity and whether the organisation or individual have prior records showing previous breaches. 


#### Photo of Australian Privacy Principles from OAIC.GOV.AU
![Australian Privacy Principles from OAIC](./screenshots/APprinciples.png)

References for Privacy Act:

Australian Privacy Principles -a summary for APP entities from 12 March 2014. (n.d.). Available at: https://www.oaic.gov.au/__data/assets/pdf_file/0020/1289/app-quick-reference-tool.pdf.

Office of the Australian Information Commissioner (2024). The Privacy Act. [online] OAIC. Available at: https://www.oaic.gov.au/privacy/privacy-legislation/the-privacy-act.

developer.atlassian.com. (n.d.). Data privacy guidelines for developers. [online] Available at: https://developer.atlassian.com/platform/marketplace/data-privacy-guidelines/.

References for Scam 2003 Act:

Australian Communications and Media Authority (2019). Spam Act | ACMA. [online] Acma.gov.au. Available at: https://www.acma.gov.au/avoid-sending-spam.


# Q9
 
The first step when creating a relational database is to create an ER (Entity-Relationship) diagram, which serves as a conceptual representation of the database structure. The ER model was created back in 1976 by Peter Chen, however over the years it has evolved into different variations. ER is very useful because it provides a clear understanding of how different entities are related before implementing data into a database. Apart from that, other benefits of ER diagram include being easy to implement and it can be done manually or websites like Draw.io and Lucidchart.

Entity Relational diagrams can be displayed in different ways, some examples include:

- Chen's notation: It consist of format shapes to describe entities and attributes. Lines and symbols are used to describe relationship connecting entities.
    - Entities are represented by rectangles.
    - Attributes are represented by ellipses.
    - Relationship are represented by lines and diamonds.
    - Primary key is underlined.


- Crow's notation: 
    - Entities are represented by rectangles.
    - Attributes are listed inside each entity's rectangle, each row describes one attribute.
    - Primary key is listed in the first row, it has an underline and it's bolded.


### Entities
Entities are Real word objects or concepts. It can be a person, place, event, objects or a concept that the tables store information about it. In database table, the entities are the 'rows'. 


### Attributes
Attributes are the characteristics that the entity is made of, the attribute's properties. In database table, the entities are the 'columns'. 

Attributes that are made of a collection of attributes are called Composite Attributes, they are represented by the *<b>oval</b>* format.


### Relationships
Relationship is the association between two or more entities that describe how they are related. Relationship generally describes 'verbs'. 

Example:
- A person HAS one passport.
- A teacher HAS many students.


### Cardinality
Defines the numerical attributes of the relationship between two entities. It represents how many instances from one entity can be associated with the instances from another entity. Cardinality can be represented by different notations. One of the most common one is the Crow's Foot Notation. It uses a single line with symbols towards the end of the line that represents the relationship type between entities.


- Crow's Foot Notation: 
    - One to One: Represented by single line with a vertical line on both ends.
    - One to Many: Represented by single line with vertical line on one end and with crow's foot on the other end.
    - Many to Many: Represented by a single line with crow's foot on both ends.

- Chen's notation:
    - One to One: Represented by '1' on both ends.
    - One to Many: Represented by '1' on one end and 'N' on the other end.
    - Many to Many: Represented by 'M' on one end and 'N' on the other end.


### Cardinality types:

- One to One:
Occurs when one entity in 'Table A' can be associated with only one entity from 'Table B', this relationship is Bi-directional. 
    - Example: A person has only one passport. A passport can be owned by only one person.
    - Example: A car has only one registration. One registration can be associated only to one car.


- One to Many:
Occurs when one entity in 'Table A' can be associated with multiple entities from 'Table B' but multiple entities from 'Table B' can be associated with only one entity from 'Table A'. This relationship is implemented by using Primary Key + Foreign Key.
    - Example: A company employs many employees, but each employee only works for one company.
    - Example: One teacher teaches many students, but each student is taught by only one teacher.


- Many to Many:
Occurs when multiple entities from 'Table A' can be associated with multiple entities from 'Table B'. When this relationship occurs, a Junction table needs to be created. Junction table is also known as Intermediate and Associate table. The Junction table contains the Foreign keys referencing the Primary keys from connected entities plus any extra attributes. Junction tables offer many benefits including data redundancy, integrity and scalability.
    - Example: Students can take many courses, courses can be taken by many students.
    - Example: Courses can have many subjects, subjects can be in many different courses.


References:

GeeksforGeeks (2015). Introduction of ER Model. [online] GeeksforGeeks. Available at: https://www.geeksforgeeks.org/introduction-of-er-model/#:~:text=For%20example%2C%20 [Accessed 1 Sep. 2024].


# Q10

Data integrity is very crucial in relational database models to ensure data stored in database is accurate and consistent. Databases are only effective when they store accurate information that can be used to provide valuable insights. It's extremely important tables are connected correctly in order to retrieve accurate information and perform operations on database. 

Applying constraints is a way to ensure integrity in Relation databases. Constraints are rules applied to database. These rules are required to be followed in order to process data correctly. A violation of constraints will cause database operations to be rejected.


### Type of constraints  

#### Primary key

Primary keys are defined in every table to uniquely identify the entities. By defining a primary key, it ensures all rows are unique and there's no redundancy. Primary key constraint automatically ensures Primary key value is not Null and indexes are unique. Attributes such as name, date and price generally can't be a primary key because it stands a chance of having a duplicate value. A example of acceptable candidate key would be ID number such as passport or driver license number. If a table doesn't contain an attribute that uniquely identify the entities, an ID primary key can be created. Only one primary key is acceptable per table.


#### Foreign Key

A foreign key is an attribute in one table that references the primary key of another table. It is used to establish and enforce a link between two tables, ensuring referential integrity. The foreign key in the child table must match the value in the primary key of the parent table (data consistency). This relational integrity ensures that any operation performed on table that contains the primary key, will automatically reflect on the table that contains the foreign key. 


#### Cascade constraint and example of Cascade in 'comments' from TRELLO API.

Cascade can be used to ensure if data is removed from parent table, it will be automatically be removed from child table. In order to use Cascade, 'timestamp' cannot be used. Values on the table that contain the foreign keys needs to be nullable in order for cascading action to work. 

Cascade in the example bellow from Trello API, ensures when a card gets deleted, the comments within that card will also be deleted.

    class Card(db.Model):
    __tablename__ = "cards"

    # Define attributes
    id = db.Column(db.Integer, primary_key =True)
    title = db.Column(db.String, nullable=False)
    description = db.Column(db.String)
    status = db.Column(db.String)
    priority = db.Column(db.String)
    date = db.Column(db.Date) # Created date
    user_id = db.Column(db.Integer, db.ForeignKey("users.id"), nullable=False)

    user = db.relationship("User", back_populates= "cards")
    comments = db.relationship("Comment", back_populates="card", cascade="all, delete")


#### DEFAULT constraint 
It can be set when no value is provided or the value is unknown, the value will default to the value provided.

    is_admin = db.Column(db.Boolean, default=False)


#### UNIQUE Constraint 
It ensures all values in the columns are unique.

    email = db.Column(db.String, nullable=False, unique=True)


#### NOT NULL constraint 
It ensures a column cannot have NULL value, it requires a value to be provided. NOT NULL should have a DEFAULT constraint to guarantee a value is assigned if none is provided.

    password = db.Column(db.String, nullable=False)


### Example of integrity methods:

Implementing foreign keys on table 'comments' from Trello API. This table requires both foreign keys from 'User'
and 'Card' tables since it reflects a many to many relationship. 

Nullable = False is set in comments table, since a comment is required to perform the operation.


    class Comment(db.Model):
  
        __tablename__ = "comments"

        id = db.Column(db.Integer, primary_key=True)
        message = db.Column(db.String, nullable=False)
        date = db.Column(db.Date)

        # Foreign keys references the Primary Key, ensures data consistency 
        user_id = db.Column(db.Integer, db.ForeignKey("users.id"), nullable=False)
        card_id = db.Column(db.Integer, db.ForeignKey("cards.id"), nullable=False)

        # Define relationship between FK and Comment model in order to get more info
        user = db.relationship("User", back_populates="comments")
        card = db.relationship("Card", back_populates="comments")


### Trello API constraints

                                    Table "public.comments"
    Column  |       Type        | Collation | Nullable |               Default                
    ---------+-------------------+-----------+----------+--------------------------------------
    id      | integer           |           | not null | nextval('comments_id_seq'::regclass)
    message | character varying |           | not null | 
    date    | date              |           |          | 
    user_id | integer           |           | not null | 
    card_id | integer           |           | not null | 
    Indexes:
        "comments_pkey" PRIMARY KEY, btree (id)
    Foreign-key constraints:
        "comments_card_id_fkey" FOREIGN KEY (card_id) REFERENCES cards(id)
        "comments_user_id_fkey" FOREIGN KEY (user_id) REFERENCES users(id)


References:

References taken from TRELLO API - Coder academy APR 2024

Microsoft (2022). Primary and Foreign Key Constraints - SQL Server. [online] learn.microsoft.com. Available at: https://learn.microsoft.com/en-us/sql/relational-databases/tables/primary-and-foreign-key-constraints?view=sql-server-ver16.

‌

# Q11

Data in relational databases can be manipulated using CRUD operations, which stands for CREATE, READ, UPDATE, and DELETE. In PostgreSQL, you retrieve data using the SELECT method, add data with the INSERT method, update data with the UPDATE method, and remove data with the DELETE method.

CLIs can also be created to perform operations on a database. Common custom commands include creating tables, seeding tables, and deleting tables. The CLI is essential for API testing because it allows you to manipulate tables directly from the API code to achieve immediate response.


#### SELECT:
The select method is used to query data from data table, SELECT * means select everything. WHERE/ FILTER BY can be used along the 'select' method to gather specific information. In the example bellow, SELECT method is used to gather information where id matches the number 1. 


SELECT DISTINCT can be be used to retrieve unique values from a specific column.

SELECT DISTINCT name FROM users;


### Example of SELECT method

    trello_db=# SELECT * FROM users WHERE id = 1;

    id |   name    |      email      |                           password                           | is_admin 
    ----+-----------+-----------------+--------------------------------------------------------------+----------
    1 | User Jess | admin@email.com | $2b$12$/pwIEBuHaPJJP/J1bpDEmOikVJh0VKzO0as2r5.cCcXp9UT2HxmNO | t
    (1 row)


#### INSERT: 

The insert method is used to insert new data into the database tables. This process can be done by using 'INSERT INTO' and 'VALUES'. 

#### Steps to perform INSERT method:

INSERT INTO name_of_the_table (Column1, Column 2, Column 3) + VALUES (Value1, Value2, Value 3) + semicolon (;) to perform the operation. 

In the TRELLO API, the first column (ID) doesn't need to entered since it has an auto-increment default value. 'IS_ADMIN' has a default value set to False. In the example above, the user 'Luke' will have default value for the attribute 'is_admin'.

If no values has conflicted with the constraints applied in database, and the operation has been successful, an acknowledgment message will be displayed confirming procedure.

- Example of a successful operation:

    trello_db=# INSERT INTO users (name, email, password)
    VALUES ('Luke', 'luke@email.com', '123456');
    INSERT 0 1

- Example of constraint's violation:

    trello_db=# INSERT INTO users (name, password)
    VALUES ('Luke', '123456');
    ERROR:  null value in column "email" of relation "users" violates not-null constraint
    DETAIL:  Failing row contains (6, Luke, null, 123456, null).
    trello_db=# 


#### UPDATE

The UPDATE method modifies existing data in tables and allows you to change one or more columns simultaneously. The WHERE clause specifies the condition to identify which row will be updated.


    UPDATE name_of_the_table
    SET column1 = value1, column2 = value2
    WHERE condition;

#### EXAMPLE TO UPDATE NAME

    trello_db=# SELECT * FROM users;

    id |  name  |      email      |                           password                           | is_admin 
    ----+--------+-----------------+--------------------------------------------------------------+----------
    1 |        | admin@email.com | $2b$12$3O1kbYcVK0n1dLxaPF22Setkg5uOLIlLZbDnZfFKeFct4L/pTH3KC | t
    2 | User A | usera@email.com | $2b$12$OFjkNTMZqqKqt9.fSquZaOonQHOtt6cutV9P68ZinU//uoXTFq9tS | f
    3 | Luke   | luke@email.com  | 123456                                                       | 
    (3 rows)

    trello_db=# UPDATE users
    trello_db-# SET name = 'User B' 
    trello_db-# WHERE id = 3;
    UPDATE 1
    
    
    trello_db=# SELECT * FROM users;

    id |    name    |      email      |                           password                           | is_admin 
    ----+------------+-----------------+--------------------------------------------------------------+----------
    1 |            | admin@email.com | $2b$12$3O1kbYcVK0n1dLxaPF22Setkg5uOLIlLZbDnZfFKeFct4L/pTH3KC | t
    2 | User A     | usera@email.com | $2b$12$OFjkNTMZqqKqt9.fSquZaOonQHOtt6cutV9P68ZinU//uoXTFq9tS | f
    3 | User B     | luke@email.com  | 123456                                                       | 
    (3 rows)

trello_db=# 


#### DELETE

The delete method deletes data from database. The WHERE clause specifies the condition to identify which row will be deleted. If no clause is specified, the delete method will delete all rows from the table.

    DELETE FROM name_of_the_table
    WHERE condition;

#### Example

    trello_db=# DELETE FROM users
    trello_db-# WHERE id = 3;
    DELETE 1
    trello_db=# 

    trello_db=# SELECT * FROM users;

    id |    name    |      email      |                           password                           | is_admin 
    ----+------------+-----------------+--------------------------------------------------------------+----------
    1 |            | admin@email.com | $2b$12$3O1kbYcVK0n1dLxaPF22Setkg5uOLIlLZbDnZfFKeFct4L/pTH3KC | t
    2 | User A     | usera@email.com | $2b$12$OFjkNTMZqqKqt9.fSquZaOonQHOtt6cutV9P68ZinU//uoXTFq9tS | f


#### Database manipulation through endpoints.

Data manipulation can also be performed through HTTP requests via an API that connects the database to endpoints (routes). POST and PATCH endpoints may include validation requirements to ensure that only appropriate data is submitted. They can also enforce authorization checks to ensure that only authorized users can perform certain operations. For instance, in the TRELLO API, only the card owner or an admin user is permitted to perform operations on cards. Bellow is the most common manipulation methods from endpoints.


#### GET request 
Equivalent to the 'SELECT' method. In the TRELLO API, this request retrieves and displays users, cards, or comments. Parameters can be used to retrieve specific information.

#### POST request
Equivalent to the 'INSERT' method, it adds new information on database. In the TRELLO API, this request is responsible for user's registration and authentication, also creates new cards and comments. 

#### PUT/PATCH request
Equivalent to the 'UPDATE' method, it updates existing data in the database. In the TRELLO API, this request is responsible for updating existing data on Users, Cards and Comments. Generally, 'PATCH' is more used since it only updates a partial part of the data, while the 'PUT' methods updates the data as a whole.

#### DELETE request 
Equivalent to the 'DELETE' method, it deletes a specific item based on the given parameter. In the TRELLO API, this request is responsible for deleting users, cards or comments.


#### POST method example from API TRELLO.
This method allows an authenticated user to create a new card. It retrieves the information from the request body and uses the 'POST' method to create a new card instance. The card schema is used to deserialize/ serialize the data from JSON into Python's understandable data and vice versa, and then the new card will be displayed to the user.

    # /cards - POST - create a new card, requires token

    @cards_bp.route("/", methods=["POST"])
    @jwt_required()

    def create_card():
        # Get the data from the body of the request
        # Load method deserialise and loads the validation from schemas
        
        card_body = card_schema.load(request.get_json())

        # Create a new card model instance
        # user_id is a foreign key in this table
        # Get user_id from token
        card = Card(
            title = card_body.get("title"),
            description = card_body.get("description"),
            date = date.today(),
            status = card_body.get("status"),
            priority = card_body.get("priority"),
            user_id = get_jwt_identity()
        )

        # Add and commit to DB
        db.session.add(card)

        db.session.commit()
        
        # Response message
        return card_schema.dump(card), 201


#### Delete method example from API TRELLO.

This method allows an authenticated user (either the card's owner or an admin user) to delete a specific card. The <int:card_id> parameter specifies which card is to be deleted. After authentication, the function retrieves the card from the database and proceeds to delete it if it exists. In both cases, the user receives an appropriate acknowledgment message.


    @cards_bp.route("/<int:card_id>", methods=["DELETE"])
    # Authorization required
    @jwt_required()
    
    def delete_card(card_id):
        # checks if user is admin or not
        is_admin = authorise_as_admin()
        # if not admin
        if not is_admin:
            # error message
            return {"error": "User is not authorised to perform this action"}
        
        # Fetch the card from DB
        stmt = db.select(Card).filter_by(id=card_id)
        card = db.session.scalar(stmt)
        
        # If card exist
        if card:    
            # Delete the card
            db.session.delete(card)
            db.session.commit()
            return {"message": f"Card {card.title} deleted successfully!"}
        # Else
        else:
            # Return error message
            return {"error": f"Card {card_id} not found."}, 404


References taken from TRELLO API - Coder academy APR 2024.


# Q12 

## FlaskBB - Flask Bulletin Board Application

## Q12-A 

### Front-End:
- HTML: Defines the structure of the application.
- CSS: Styles the application.
- Jinja2: Python's web template engine used for rendering dynamic HTML.
- JavaScript: Programming language used to create interactive content.

### Back-End:

- Python: Programming language used to develop the application.
- Flask: Python's micro web framework used to build the web application and API.
- SQLAlchemy: Object Relational Mapper to connect the application to the database.
- Flask-Login: An extension used for managing user sessions and authentication.
- Flask-Migrate: A Flask extension that handles SQLAlchemy database migrations, allowing changes to the database schema.
- Databases: Stores, manages and retrieve data related to Users and Forums.
    - SQLite: Default database. 
    - Also supported: PostgreSQL and MySQL.

- Git: Version control system used to track application's code progress. Ir allows collaboration between developers.
- Virtual Environment: Used to isolate the project’s dependencies.
- Pip: Manager package used to install dependencies to run the application.
- 

References:

flaskbb (2024). flaskbb/requirements.txt at master · flaskbb/flaskbb. [online] GitHub. Available at: https://github.com/flaskbb/flaskbb/blob/master/requirements.txt [Accessed 8 Sep. 2024].

flaskbb (2014). flaskbb/flaskbb/configs/default.py at master · flaskbb/flaskbb. [online] GitHub. Available at: https://github.com/flaskbb/flaskbb/blob/master/flaskbb/configs/default.py [Accessed 8 Sep. 2024].

‌
flaskbb (2024). flaskbb/flaskbb/templates/layout.html at master · flaskbb/flaskbb. [online] GitHub. Available at: https://github.com/flaskbb/flaskbb/blob/master/flaskbb/templates/layout.html [Accessed 8 Sep. 2024].

‌
Readthedocs.io. (2022). Installation — FlaskBB Documentation. [online] Available at: https://flaskbb.readthedocs.io/en/latest/installation.html#id1 [Accessed 8 Sep. 2024].

flaskbb (2014). flaskbb/flaskbb/app.py at master · flaskbb/flaskbb. [online] GitHub. Available at: https://github.com/flaskbb/flaskbb/blob/master/flaskbb/app.py [Accessed 8 Sep. 2024].

‌

### Q12-B

- First step: 
Create a Virtual Environment:
Purpose: Keeps dependencies isolated.
Setup: Install virtualenv and virtualenvwrapper. Activate virtual environment after creating it.

- Second step: 
Instal the dependencies:
Install: Use pip to install FlaskBB’s dependencies from requirements.txt and requirements-dev.txt (extra dependencies required for development).

- Third step: 
Configuration:
Create Config: Use the command 'flaskbb makeconfig' to generate a configuration file.
Modify the following variables: Update the configuration file with settings like SERVER_NAME, SQLALCHEMY_DATABASE_URI, SECRET_KEY, and WTF_CSRF_SECRET_KEY.

### Deployment (Supervisor + uWSGI + nginx)

- Servers:
Application Server: Runs the FlaskBB app (using uWSGI or Gunicorn). According to the official documentation Gunicorn is the easiest method to run a FlaskBB instance.
Web Server: Handles user requests and serves files (using nginx).

- Software Setup:
Supervisor: Keeps the application server running.
uWSGI/Gunicorn: Software that runs your FlaskBB app.
nginx: Handles incoming requests and serves static files.

- PythonAnywhere:
Easy way to run FlaskBB. Create an account with PythonAnywhere and proceed with the configuration by git clone and install. All steps are listed on FlaskBB installation page.


References:

Readthedocs.io. (2022). Installation — FlaskBB Documentation. [online] Available at: https://flaskbb.readthedocs.io/en/latest/installation.html#id5 [Accessed 8 Sep. 2024].

flaskbb (2024). flaskbb/docs/installation.rst at master · flaskbb/flaskbb. [online] GitHub. Available at: https://github.com/flaskbb/flaskbb/blob/master/docs/installation.rst [Accessed 8 Sep. 2024].



## Q12 - C

Flask is the core of the FlaskBB application. It handles HTTP requests and routes them to specific functions based on URL patterns. In FlaskBB, when a user requests to view a specific forum, Flask processes the request and generates the appropriate response. To gather the necessary data, Flask interacts with the database through SQLAlchemy. FlaskBB uses SQLite as its default database but can also be configured to work with other databases like PostgreSQL or MySQL. The user interface is built with HTML, CSS, Jinja2, and JavaScript. HTML provides the structure of the pages, CSS is responsible for the styling, and JavaScript adds interactivity. FlaskBB also uses Bootstrap, a front-end framework that ensures a responsive design, adapting the application for different screen sizes and devices.

SQLAlchemy connects the Flask application to the database via Object-Relational Mapping (ORM). This allows developers to use Python classes to represent database tables, where each class corresponds to a table, and the class attributes represent table columns. SQLAlchemy also handles CRUD (Create, Read, Update, Delete) operations, allowing FlaskBB to interact with the database in a structured way. FlaskBB uses Flask-Migrate, an extension that helps manage database schema changes without data loss, by generating migration scripts whenever changes are made. Additionally, FlaskBB uses Flask-Login to manage user authentication. Flask-Login handles user logins, logout, and session management, ensuring secure access control throughout the application.

Git is used for version control and collaboration in FlaskBB development. It allows developers to contribute to the project by submitting pull requests, reporting bugs, or suggesting new features. Contributions are managed through GitHub, where developers can review, track, and merge code changes.

FlaskBB supports plugins and extensions, which make the application highly customizable. Developers can easily add new features or modify existing functionality through plugins, making it simple to adapt FlaskBB to specific needs without modifying its core codebase.


### Q12-D

In FlaskBB, the data is structured via the Object relational mapping, which organise the data into different tables. Each table represents a specific entity, such as users, groups, forums, moderators.

### User
Users are the individuals who interact with the forum.

- Attributes:

- Id: Unique identifier for the user.
- Username: Unique username.
- Email: Email address.
- Password: Password for authentication.
- Joined_on: Timestamp of when the user joined.

- Relationship:
- Posts: One-to-Many (a user can create many posts).
- Groups: Many-to-Many (users can belong to multiple groups).

### Group
Groups represent roles or categories of users.

- Attributes:
- Id: Unique identifier for the group.
Name: Name of the group (e.g., Admin, Moderator).
Permissions: Permissions associated with the group.

- Relationship:
A group can have many users, many groups can have many users.

### Forum
Forums are the discussion areas in the application.

- Attributes:
- Id: Unique identifier for the forum.
- Name: Name of the forum.
- Description: Description of the forum.
- Category_id: Foreign key to the Category to which the forum belongs.


### Q12-E

### Groups table

    class Group(db.Model, CRUDMixin):
        __tablename__ = "groups"

        id = db.Column(db.Integer, primary_key=True)
        name = db.Column(db.String(255), unique=True, nullable=False)
        description = db.Column(db.Text, nullable=True)

        # Group types
        admin = db.Column(db.Boolean, default=False, nullable=False)
        super_mod = db.Column(db.Boolean, default=False, nullable=False)
        mod = db.Column(db.Boolean, default=False, nullable=False)
        guest = db.Column(db.Boolean, default=False, nullable=False)
        banned = db.Column(db.Boolean, default=False, nullable=False)


### Users table
    class User(db.Model, UserMixin, CRUDMixin):
        __tablename__ = "users"

        id = db.Column(db.Integer, primary_key=True)
        username = db.Column(db.String(200), unique=True, nullable=False)
        email = db.Column(db.String(200), unique=True, nullable=False)
        _password = db.Column("password", db.String(120), nullable=False)
        date_joined = db.Column(UTCDateTime(timezone=True), default=time_utcnow, nullable=False)


### Forums table
    class Forum(db.Model, CRUDMixin):
        __tablename__ = "forums"

        id = db.Column(db.Integer, primary_key=True)
        category_id = db.Column(
            db.Integer, db.ForeignKey("categories.id", ondelete="CASCADE"), nullable=False
        )
        title = db.Column(db.String(255), nullable=False)
        description = db.Column(db.Text, nullable=True)
        position = db.Column(db.Integer, default=1, nullable=False)
        locked = db.Column(db.Boolean, default=False, nullable=False)
        show_moderators = db.Column(db.Boolean, default=False, nullable=False)
        external = db.Column(db.String(200), nullable=True)

        post_count = db.Column(db.Integer, default=0, nullable=False)
        topic_count = db.Column(db.Integer, default=0, nullable=False)


### Q12-F

<b> User to Group: Many-to-Many (through the groups_users table)</b>

<b> Group to User: Many-to-Many (through the groups_users table)</b>

    groups_users = db.Table(
        "groups_users",
        db.Column(
            "user_id",
            db.Integer,
            db.ForeignKey("users.id", ondelete="CASCADE"),
            nullable=False,
        ),
        db.Column(
            "group_id",
            db.Integer,
            db.ForeignKey("groups.id", ondelete="CASCADE"),
            nullable=False,
        ),
    )



<b>Group to Forum: Many-to-Many (through the forumgroups table)</b>

<b>Forum to Group: Many-to-Many (through the forumgroups table)</b>

        forumgroups = db.Table(
            "forumgroups",
            db.Column(
                "group_id",
                db.Integer(),
                db.ForeignKey("groups.id", ondelete="CASCADE"),
                nullable=False,
            ),
            db.Column(
                "forum_id",
                db.Integer(),
                db.ForeignKey("forums.id", ondelete="CASCADE"),
                nullable=False,
            ),
        )



<b>User to Forum: Many-to-Many (through the moderators table) </b>

<b>Forum to User: Many-to-Many (through the moderators table) </b>

    moderators = db.Table(
        "moderators",
        db.Column(
            "user_id",
            db.Integer(),
            db.ForeignKey("users.id", ondelete="CASCADE"),
            nullable=False,
        ),
        db.Column(
            "forum_id",
            db.Integer(),
            db.ForeignKey("forums.id", ondelete="CASCADE"),
            nullable=False,
        ),
    )


### Q12-G

![Screenshot](./screenshots/Q12.png)

References for Q12:

flaskbb (2024). flaskbb/flaskbb at master · flaskbb/flaskbb. [online] GitHub. Available at: https://github.com/flaskbb/flaskbb/tree/master/flaskbb [Accessed 8 Sep. 2024].

‌