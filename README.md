# Project - workbook (t2) Part A
Submit a day or two days before to check for Turnitin. 

# Q1 - mark 6
Describe the architecture of a typical API project, such as a Flask application.


# Q2 - mark 6
Identify a database commonly used in an API project (such as a Flask application) and discuss the pros and cons of this database.



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
System and data redundancy are another important measures organisations can use to make sure their data is complete and operations can be handled in case of failure/loss. Often backups and multiple copies in different systems or locations can also be beneficial to ensure if their suffer an cyber attack they don't have a total loss of data.


- Availability:
This component ensures the data is available all the time to authorised users for viewing and modifications when it needed. To ensure maximum availability, the system must be safe from malicious activities and data should be stored/managed safely. This component goes side by side with confidentiality and integrity components. Some measures to make this happen includes conducting regular system maintenance updates, implements measures to protect against malicious attacks, make use of data and system redundancy, have a recovery plan, use of Load balancers to distribute incoming traffic across multiple servers and preventing one server to become overwhelmed resulting in better performance. Load balance softwares includes HAProxy and NGINX or Cloud-based includes AWS Elastic and Azure. Recover plans can include risk assessments to identify threats and potential risks, and recovery procedures to indicate what steps to take in case of data/ system disruption.

REF: https://www.infosecurityeurope.com/en-gb/blog/guides-checklists/principles-of-information-security.html

# Q7 - mark 6
Provide an overview of what would need to be done within an API project to implement at least one of the principles explained in Question 6.


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


