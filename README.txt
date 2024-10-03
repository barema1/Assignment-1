BAREMA GAEL 26255
DOCUMENTATION

A relational database is used by the system to manage users, groups, roles, systems, and events. It monitors roles and their descriptions (e.g., Admin, User, Guest), and it has tables for users with attributes like username, password, and email. Users can be grouped into communities using groups, and systems can be used to record information about the different tools or functionalities under management. Events record system activity, and key-value pairs are associated with particular systems via the `Properties` table.

Role-based access restriction is made possible by the `UserRoles` table, which links users to roles. To provide system accountability and traceability, user or system actions are recorded in an events table. Primary and foreign keys are used to enforce data integrity and guarantee appropriate relationships between tables. 


In general, the system is made to monitor system activity, assign group memberships, manage user responsibilities, and enforce access control through a strong relational structure.



Here below are the Queries:

SQL> CREATE TABLE Users (
  2    2  user_id INT PRIMARY KEY,
  3    3  username VARCHAR2(50) UNIQUE,
  4    4  password VARCHAR2(255),
  5    5  email VARCHAR2(100),
  6    6  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
  7    6  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP^Z^Z^ZCREATE TABLE Users (
  2  user_id INT PRIMARY KEY,
  8    3  username VARCHAR2(50) UNIQUE,
  9    4  password VARCHAR2(255),
 10    5  email VARCHAR2(100),
 11    6  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
 12
SQL>
SQL> CREATE TABLE Users (
  2      user_id INT PRIMARY KEY,
  3      username VARCHAR2(50) UNIQUE,
  4      password VARCHAR2(255),
  5      email VARCHAR2(100),
  6      created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
  7     );

Table created.

SQL> CREATE TABLE Roles (
  2      role_id INT PRIMARY KEY,
  3      name VARCHAR2(50),
  4      description CLOB
  5      );

Table created.

SQL> CREATE TABLE Groups (
  2      group_id INT PRIMARY KEY,
  3      name VARCHAR2(50),
  4      description CLOB
  5      );

Table created.

SQL> CREATE TABLE Systems (
  2      system_id INT PRIMARY KEY,
  3      name VARCHAR2(100),
  4      description CLOB
  5      );

Table created.

SQL> CREATE TABLE Properties (
  2      property_id INT PRIMARY KEY,
  3      system_id INT,
  4      name VARCHAR2(100),
  5      value CLOB,
  6      CONSTRAINT fk_system_id FOREIGN KEY (system_id) REFERENCES Systems(syst
  7  em_id)
  8      );
em_id)
*
ERROR at line 7:
ORA-00907: missing right parenthesis


SQL> CREATE TABLE Properties (
  2      property_id INT PRIMARY KEY,
  3      system_id INT,
  4      name VARCHAR2(100),
  5      value CLOB,
  6      CONSTRAINT fk_system_id FOREIGN KEY (system_id) REFERENCES Systems(system_id)
  7      );

Table created.

SQL> CREATE TABLE Events (
  2      event_id INT PRIMARY KEY,
  3      system_id INT,
  4      type VARCHAR2(50),
  5      message CLOB,
  6      timestamp TIMESTAMP,
  7      CONSTRAINT fk_events_system_id FOREIGN KEY (system_id) REFERENCES Systems(system_id)
  8      );

Table created.

SQL> CREATE TABLE Actions (
  2    2  action_id INT PRIMARY KEY,
  3    3  system_id INT,
  4    4  type VARCHAR2(50),
  5    5  message CLOB,
  6    6  timestamp TIMESTAMP,
  7    7  CONSTRAINT fk_actions_system_id FOREIGN KEY (system_id) REFERENCES Syst
  8  ems(system_id)
  9    8  );
  2  action_id INT PRIMARY KEY,
  *
ERROR at line 2:
ORA-00904: : invalid identifier


SQL> CREATE TABLE Actions (
  2      action_id INT PRIMARY KEY,
  3      system_id INT,
  4      type VARCHAR2(50),
  5      message CLOB,
  6      timestamp TIMESTAMP,
  7      CONSTRAINT fk_actions_system_id FOREIGN KEY (system_id) REFERENCES Systems(system_id)
  8      );

Table created.

SQL> Inserting a new user
SP2-0734: unknown command beginning "Inserting ..." - rest of line ignored.
SQL> INSERT INTO Users (user_id, username, password, email, created_at)
  2  VALUES (1, 'john_doe', 'hashed_password_1', 'john@example.com', SYSTIMESTAMP);

1 row created.

SQL>
SQL> INSERT INTO Users (user_id, username, password, email, created_at)
  2  VALUES (2, 'jane_smith', 'hashed_password_2', 'jane@example.com', SYSTIMESTAMP);

1 row created.

SQL>
SQL> INSERT INTO Users (user_id, username, password, email, created_at)
  2  VALUES (3, 'alice_jones', 'hashed_password_3', 'alice@example.com', SYSTIMESTAMP);

1 row created.

SQL> INSERT INTO Roles (role_id, name, description)
  2  VALUES (1, 'Admin', 'Administrator role with full access');

1 row created.

SQL>
SQL> INSERT INTO Roles (role_id, name, description)
  2  VALUES (2, 'User', 'Regular user with limited access');

1 row created.

SQL>
SQL> INSERT INTO Roles (role_id, name, description)
  2  VALUES (3, 'Guest', 'Guest user with read-only access');

1 row created.

SQL> INSERT INTO Groups (group_id, name, description) VALUES
  2  (1, 'Book Club', 'A group for people who love reading and discussing books.');

1 row created.

SQL> (2, 'Hiking Enthusiasts', 'A community for those who enjoy outdoor adventures and hiking.');
(2, 'Hiking Enthusiasts', 'A community for those who enjoy outdoor adventures and hiking.')
 *
ERROR at line 1:
ORA-00928: missing SELECT keyword


SQL> (3, 'Photography Lovers', 'A group for amateur and professional photographers to share their work and tips.');
(3, 'Photography Lovers', 'A group for amateur and professional photographers to share their work and tips.')
 *
ERROR at line 1:
ORA-00928: missing SELECT keyword


SQL> (4, 'Tech Innovators', 'A network for individuals interested in technology and innovation.');
(4, 'Tech Innovators', 'A network for individuals interested in technology and innovation.')
 *
ERROR at line 1:
ORA-00928: missing SELECT keyword


SQL> (5, 'Cooking Masters', 'A group dedicated to cooking and sharing recipes from around the world.');
(5, 'Cooking Masters', 'A group dedicated to cooking and sharing recipes from around the world.')
 *
ERROR at line 1:
ORA-00928: missing SELECT keyword


SQL> INSERT INTO Groups (group_id, name, description) VALUES(2, 'Hiking Enthusiasts', 'A community for those who enjoy outdoor adventures and hiking.');

1 row created.

SQL> INSERT INTO Groups (group_id, name, description) VALUES(3, 'Photography Lovers', 'A group for amateur and professional photographers to share their work and tips.');

1 row created.

SQL> INSERT INTO Groups (group_id, name, description) VALUES(4, 'Tech Innovators', 'A network for individuals interested in technology and innovation.');

1 row created.

SQL> INSERT INTO Groups (group_id, name, description) VALUES(5, 'Cooking Masters', 'A group dedicated to cooking and sharing recipes from around the world.');

1 row created.

SQL> INSERT INTO Systems (system_id, name, description) VALUES(1, 'Inventory Management', 'A system for tracking inventory levels, orders, sales, and deliveries.');

1 row created.

SQL> INSERT INTO Systems (system_id, name, description) VALUES(2, 'Customer Relationship Management', 'A system for managing a company\'s interactions with current and potential customers.');
ERROR:
ORA-01756: quoted string not properly terminated


SQL> INSERT INTO Systems (system_id, name, description) VALUES(3, 'Project Management Tool', 'A system designed to help manage project planning, resources, and schedules.');

1 row created.

SQL> INSERT INTO Systems (system_id, name, description) VALUES(4, 'Financial Accounting System', 'A system that helps manage financial transactions and reporting.');

1 row created.

SQL> INSERT INTO Systems (system_id, name, description) VALUES(5, 'Human Resource Management', 'A system for managing employee data, recruitment, and payroll processes.');

1 row created.

SQL> INSERT INTO Systems (system_id, name, description) VALUES(2, 'Customer Relationship Management', 'A system for managing a company's interactions with current and potential customers.');
ERROR:
ORA-01756: quoted string not properly terminated


SQL> INSERT INTO Systems (system_id, name, description) VALUES(2, 'Customer Relationship Management', 'A system for managing a companys interactions with current and potential customers.');

1 row created.

SQL>
SQL> UPDATE Roles
  2  SET description = 'Administrator role with full access and management capabilities'
  3  WHERE role_id = 1;

1 row updated.

SQL>
SQL>
SQL> UPDATE Roles
  2  SET description = 'Regular user with limited access to features'
  3  WHERE role_id = 2;

1 row updated.

SQL>
SQL>
SQL> UPDATE Roles
  2  SET description = 'Guest user with read-only access to public content'
  3  WHERE role_id = 3;

1 row updated.

SQL> DELETE FROM Users
  2  WHERE user_id = 2;

1 row deleted.

SQL> CREATE TABLE UserRoles (
  2      user_id INT,
  3      role_id INT,
  4      PRIMARY KEY (user_id, role_id),
  5      FOREIGN KEY (user_id) REFERENCES Users(user_id),
  6      FOREIGN KEY (role_id) REFERENCES Roles(role_id)
  7  );

Table created.

SQL> INSERT INTO UserRoles (user_id, role_id) VALUES(1, 1),  -- User ID 1 assigned to Role ID 1 (e.g., Admin);
INSERT INTO UserRoles (user_id, role_id) VALUES(1, 1),  -- User ID 1 assigned to Role ID 1 (e.g., Admin)
                                                     *
ERROR at line 1:
ORA-00933: SQL command not properly ended


SQL> INSERT INTO UserRoles (user_id, role_id) VALUES(1, 2),  -- User ID 1 also assigned to Role ID 2 (e.g., User);
INSERT INTO UserRoles (user_id, role_id) VALUES(1, 2),  -- User ID 1 also assigned to Role ID 2 (e.g., User)
                                                     *
ERROR at line 1:
ORA-00933: SQL command not properly ended


SQL> INSERT INTO UserRoles (user_id, role_id) VALUES(2, 2),  -- User ID 2 assigned to Role ID 2 (e.g., User);
INSERT INTO UserRoles (user_id, role_id) VALUES(2, 2),  -- User ID 2 assigned to Role ID 2 (e.g., User)
                                                     *
ERROR at line 1:
ORA-00933: SQL command not properly ended


SQL> INSERT INTO UserRoles (user_id, role_id) VALUES(3, 3);  -- User ID 3 assigned to Role ID 3 (e.g., Guest);
INSERT INTO UserRoles (user_id, role_id) VALUES(3, 3);  -- User ID 3 assigned to Role ID 3 (e.g., Guest)
                                                     *
ERROR at line 1:
ORA-00933: SQL command not properly ended


SQL> INSERT INTO UserRoles (user_id, role_id) VALUES(1, 1);

1 row created.

SQL> INSERT INTO UserRoles (user_id, role_id) VALUES(1, 2);

1 row created.

SQL> INSERT INTO UserRoles (user_id, role_id) VALUES(2, 2);
INSERT INTO UserRoles (user_id, role_id) VALUES(2, 2)
*
ERROR at line 1:
ORA-02291: integrity constraint (SYS.SYS_C008326) violated - parent key not
found


SQL> INSERT INTO UserRoles (user_id, role_id) VALUES(2, 2);
INSERT INTO UserRoles (user_id, role_id) VALUES(2, 2)
*
ERROR at line 1:
ORA-02291: integrity constraint (SYS.SYS_C008326) violated - parent key not
found


SQL> INSERT INTO UserRoles (user_id, role_id) VALUES(3, 3);

1 row created.

SQL> SELECT
  2      u.user_id,
  3      u.username,
  4      u.email,
  5      r.name AS role_name,
  6      r.description AS role_description
  7  FROM
  8      Users u
  9  INNER JOIN
 10      UserRoles ur ON u.user_id = ur.user_id
 11  INNER JOIN
 12      Roles r ON ur.role_id = r.role_id;

   USER_ID USERNAME
---------- --------------------------------------------------
EMAIL
--------------------------------------------------------------------------------
ROLE_NAME
--------------------------------------------------
ROLE_DESCRIPTION
--------------------------------------------------------------------------------
         1 john_doe
john@example.com
Admin
Administrator role with full access and management capabilities


   USER_ID USERNAME
---------- --------------------------------------------------
EMAIL
--------------------------------------------------------------------------------
ROLE_NAME
--------------------------------------------------
ROLE_DESCRIPTION
--------------------------------------------------------------------------------
         1 john_doe
john@example.com
User
Regular user with limited access to features


   USER_ID USERNAME
---------- --------------------------------------------------
EMAIL
--------------------------------------------------------------------------------
ROLE_NAME
--------------------------------------------------
ROLE_DESCRIPTION
--------------------------------------------------------------------------------
         3 alice_jones
alice@example.com
Guest
Guest user with read-only access to public content


SQL> INSERT INTO Users (user_id, username, password, email) VALUES
  2  (4, 'bob_brown', 'hashed_password_4', 'bob@gmail.com');

1 row created.

SQL> INSERT INTO Roles (role_id, name, description) VALUES
  2  (4, 'Moderator', 'Moderates content and user interactions.');

1 row created.

SQL> UPDATE Users
  2  SET email = 'john_doe_updated@example.com'
  3  WHERE username = 'john_doe';

1 row updated.

SQL> DELETE FROM Roles
  2  WHERE role_id = 4;

1 row deleted.

SQL> SELECT
  2      u.user_id,
  3      u.username,
  4      r.name AS role_name
  5  FROM
  6      Users u
  7  LEFT JOIN
  8      UserRoles ur ON u.user_id = ur.user_id
  9  LEFT JOIN
 10      Roles r ON ur.role_id = r.role_id;

   USER_ID USERNAME
---------- --------------------------------------------------
ROLE_NAME
--------------------------------------------------
         1 john_doe
Admin

         1 john_doe
User

         3 alice_jones
Guest


   USER_ID USERNAME
---------- --------------------------------------------------
ROLE_NAME
--------------------------------------------------
         4 bob_brown



SQL> SELECT
  2      r.name AS role_name,
  3      COUNT(u.user_id) AS user_count
  4  FROM
  5      Roles r
  6  LEFT JOIN
  7      (SELECT ur.user_id, ur.role_id
  8       FROM UserRoles ur) user_roles ON r.role_id = user_roles.role_id
  9  LEFT JOIN
 10      Users u ON user_roles.user_id = u.user_id
 11  GROUP BY
 12      r.name;

ROLE_NAME                                          USER_COUNT
-------------------------------------------------- ----------
Admin                                                       1
User                                                        1
Guest                                                       1