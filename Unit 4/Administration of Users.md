## Administering Users in SQL Server

### Introduction

Effective user administration is crucial for database systems like SQL Server to ensure authorized access and protect sensitive data. This involves managing user accounts and their permissions.

### Authentication

**Authentication** is the process of verifying the identity of a user or entity. Before granting access to a database, SQL Server uses authentication to confirm the user's identity.

**Authentication Methods:**

- **Windows Authentication:** This method relies on the Windows operating system's authentication mechanisms, such as Active Directory. It is considered more secure due to its leverage of OS-level security policies and potential for multi-factor authentication.
- **SQL Server Authentication:** This method requires a specific SQL Server login and password for authentication. It is typically used when Windows Authentication isn't feasible. However, it is considered less secure compared to Windows Authentication.

**Example: SQL Server Authentication with Password Policy**

```
CREATE LOGIN TestUser
WITH PASSWORD = 'StrongPassword123!',
CHECK_POLICY = ON,
CHECK_EXPIRATION = ON;
```

This SQL code demonstrates creating a new login (`TestUser`) with a strong password. The inclusion of `CHECK_POLICY = ON` and `CHECK_EXPIRATION = ON` ensures that the login adheres to the system's password policies.

### Creating Users

After creating a login, a database user needs to be associated with it to enable access to specific databases.

**Example: Creating a Database User from a Login**

```
USE TestDatabase;
CREATE USER TestUser
FOR LOGIN TestUser;
```

This code associates the `TestUser` login with the `TestDatabase`, granting the user access to that database based on the permissions granted.

### Removing and Modifying Users

User administration involves modifying or removing user accounts as needed to ensure that obsolete or unauthorized users no longer have system access.

**Example: Dropping a User from a Database**

```
USE TestDatabase;
DROP USER TestUser;
```

Before dropping a user, ensure all permissions are revoked, and associated roles are removed.

### Default Users and Remote Users

SQL Server includes default accounts, like the `sa` account, with system-level access. These accounts should have strong security measures to prevent unauthorized access. Databases often require connections from remote users or servers.

### Database Links

**Remote Users:** Users connecting to the database from locations outside the server.

**Linked Servers:** Enable querying across databases on different servers.

**Example: Creating a Linked Server**

```
EXEC sp_addlinkedserver
@server = 'RemoteServer',
@srvproduct = '',
@provider = 'SQLNCLI',
@datasrc = 'remote.database.server';
```

This code creates a linked server to execute queries on a remote server (`RemoteServer`), facilitating integration across multiple systems.

### Best Practices for Administrators

- **Strong, unique passwords:** Essential to protect against password-based attacks.
- **Principle of least privilege:** Grant only the minimum necessary privileges for users to perform their tasks.
- **User activity auditing:** Log and review user actions for any suspicious patterns or privilege escalation attempts.
- **Regular user access reviews:** Ensure users only retain necessary permissions.

### Profiles

SQL Server utilizes profiles to manage system resource usage, limiting CPU and memory consumption per user. These profiles are managed using the Resource Governor.

**Example: Creating Resource Pools and Workload Groups**

```
CREATE RESOURCE POOL CustomPool
WITH (MIN_CPU_PERCENT = 10, MAX_CPU_PERCENT = 50);

CREATE WORKLOAD GROUP CustomGroup
USING CustomPool;

ALTER RESOURCE GOVERNOR RECONFIGURE;
```

This code establishes a resource pool (`CustomPool`) and a workload group (`CustomGroup`) to control resource use. This setup enforces CPU limits for queries from that group via the Resource Governor.

### Password Policies

A robust password policy is vital to database security. SQL Server allows enforcing password policies, such as length, complexity, expiration, and lockout settings.

**Password Policy Best Practices:**

- **Minimum length:** Passwords should be at least 8 characters long.
- **Complexity:** Enforce using uppercase, lowercase, numbers, and special characters.
- **Expiration:** Set a password expiration, such as every 90 days.
- **Account lockout:** Configure a lockout mechanism after multiple failed login attempts to prevent brute-force attacks.
