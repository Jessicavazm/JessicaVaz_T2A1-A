# Project - workbook (t2) Part A
Submit a day or two days before to check for Turnitin. 

# Q1 - mark 6
Describe the architecture of a typical API project, such as a Flask application.
Flask

# Q2 - mark 6
Identify a database commonly used in an API project (such as a Flask application) and discuss the pros and cons of this database.

## PostgreSQL
PostgreSQL was created back in 1986 at the University of California, Berkeley. Originally the system was named POSTGRES in relation to the Ingres database which was also developed in the same university. Later on, in 1996 the project was renamed from Postgres to PostgreSQL to reflect the support to SQL (Structure query language). The project was created under the professor Michael Stone breaker. PostgreSQL is one of the most older database systems and it's extremely popular due to it's reliability and architecture. It's an open source database system which means it's not owned by a single company or owner and source code can be accessed by anyone. The database system is managed by a group of developers and volunteers called PostgreSQL Global Development Group. 
PostgreSQL is currently on version 16, with version 16.4 released on August 8, 2024.<br>

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
- Since PostgreSQL is an open source and not owned by a particular organisation, the database software does not carry liability for damages or offers warranty of any kind.
- Due to it's vast number of functionalities which is also considered a strong feature, it can be intimidating to users who are new to the system or users who don't have much experience with relational databases systems.
- Performance can be considered slower than SQL Server and MySQL.

Sources: <br>
https://www.postgresql.org/about/ <br>
https://aws.amazon.com/rds/postgresql/what-is-postgresql/ <br>
https://www.aalpha.net/blog/pros-and-cons-of-using-postgresql-for-application-development/ <br>
https://cloud.google.com/learn/postgresql-vs-sql <br>

# Q3 - mark 6
Discuss an implementation of an Agile project management methodology for an API project.



# Q4 - mark 6
Provide an overview and description of a standard source control process for an API project.



# Q5 - mark 6
Provide an overview and description of a standard testing process for an API project.



# Q6 - mark 6
Explain the three principles of information system security.
CIA triad is an Information system security model that has 3 core principles: Confidentiality, Integrity and Availability. This model is widely used by organisations and it's main purpose is to keep data secure. The three components corelate to each other.

- Confidentiality: 
It ensures data is only accessible to view and edit to authorised users by implementing control's measures such as authentication, encryption and data masking. Authentication method ensures user's identification, it can be done through username and password, tokens, biometric identifiers such as fingerprint or facial and plenty more. Encryption methods ensures data is secured in the transit process by making it unreadable. When you encrypt a file, it generates a key which is only granted to authorised users. With this key, users are able to convert message to the original format and read it. Masking is another method that involves replacing the original data with a fictional data. Monitoring data is also another important process in the confidentiality method. Organisations can use applications such as Intrusion detection system (IDS) and Intrusion prevention system (IPS) to prevent and report any malicious activity. Another powerful tool is to report security incidents, this can also help to identify any security breach that might occur in the future. For this reason, employees should be trained and be aware of security breaches types and best practices to be able to identify any future problem and understand how to handle data securely.


- Integrity: 
This component is responsible for data's integrity during transit or rest processes. Some techniques to help with integrity are checksum and hash functions. Checksum is unique value that is generated after processing the original data, in case of an accidental error, a different checksum will be generated indicating the data has been altered. Hash function converts a file to fixed strings of bytes(Hexadecimal). Like Checksum, the Hash function produces a unique value that is used to check if data has been modified.<br>
Version control system such as GIT is also used as a method to ensure data integrity, allowing users to track all changes and restore previous version if needed.
System and data redundancy are another important measures organisations can use to make sure their data is complete and operations can be maintain in case of failure/loss. Often backups and multiple copies in different systems or locations can also be beneficial to ensure if their suffer an cyber attack they don't have a total loss of data.


- Availability:
This component ensures the data is available all the time to authorised users for viewing and modifications when it needed. To ensure maximum availability, the system must be safe from malicious activities and data should be stored/managed safely. This component goes side by side with confidentiality and integrity components. Some measures to make this happen includes conducting regular system maintenance updates, implements measures to protect against malicious attacks, make use of data and system redundancy, have a recovery plan, use of Load balancers to distribute incoming traffic across multiple servers and preventing one server to become overwhelmed resulting in better performance. Load balance softwares includes HAProxy and NGINX or Cloud-based includes AWS Elastic and Azure. Recover plans can include risk assessments to identify threats and potential risks, and recovery procedures to indicate what steps to take in case of data/ system disruption.

REF: https://www.infosecurityeurope.com/en-gb/blog/guides-checklists/principles-of-information-security.html

# Q7 - mark 12
Provide an overview of what would need to be done within an API project to implement at least one of the principles explained in Question 6.

- Component `Confidentiality`



# Q8 - mark 12 (second main question)
Explain the legal obligations that developers of a social media website or social media application would have in regards to handling user data, with reference to any applicable laws or acts.



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


