---
layout: post
title: Understand PostreSQL roles, users and privileges
date: 2019-08-09
---

I looked at postgreSQL 11 (but it should be the same for older versions ?)

# Roles

Postgres manages database access permissions using **roles**.

A **role** can be a database **user** or a **group** of database users,
depending on how you setup the role. To create a role:

    CREATE ROLE role_name;

A **user** is a role with **login** privilege. To create a user:

    CREATE USER user_name PASSWORD 'password';
    -- or
    CREATE ROLE user_name LOGIN PASSWORD 'password'

## Role attributes

A role has **attributes** that define its privileges and interact with the client
authentication system:

* `LOGIN`: allows a role to log in a database
* `SUPERUSER`: superuser status, bypasses all permission checks, except the right to log in
* `CREATEDB`: allows a role to create databases
* `CREATEROLE`: allows a role to create other roles
* `REPLICATION LOGIN`: initial streaming replication 
* `PASSWORD`: defines a password for a role

Note that role-specific defaults attached to roles without LOGIN privilege are
fairly useless, since they will never be invoked.

    CREATE ROLE name LOGIN; -- equivalent to CREATE USER name;
    CREATE ROLE name SUPERUSER;
    CREATE ROLE name CREATEDB;
    CREATE ROLE name CREATEROLE;
    CREATE ROLE name REPLICATION LOGIN;
    CREATE ROLE name PASSWORD 'string';

## Ownership

When an object is created, it is assigned an **owner**. The **owner** is
normally the **role** that executed the **creation statement**.

An object can be assigned to a new owner with an `ALTER` command.

### Privileges

The initial state is that **only** the owner (or a superuser) can do anything with
the object. To allow other roles to use it, privileges must be granted. The
owner has some special privileges that only him and superusers have (`DROP`, 
`GRANT`, `REVOKE`, etc.), these privileges cannot be granted or revoked.

The privileges are:

* `SELECT`: allows select
* `INSERT`: allows insert
* `UPDATE`: allows update
* `DELETE`: allows delete
* `TRUNCATE`: allows truncate
* `REFERENCES`: allows creation of a foreign key constraint
* `TRIGGER`: allows the creation of a trigger
* `CREATE`: depends on the object (go check the [doc](https://www.postgresql.org/docs/11/sql-grant.html))
* `CONNECT`: allows the user to connect to the specified database
* `TEMPORARY`: allows temporary tables to be created
* `EXECUTE`: allows the use of the specified function or procedure, or any
operators on top of the function
* `USAGE`: depends on the object, but on schemas, allows access to objects
contained in the specified schema
* `ALL PRIVILEGES`: Grant all of the available privileges at once

The right to modify or destroy an object is always the privilege of the owner only.

* `GRANT PERMISION ON object TO user` ex of granting privileges
* `REVOKE ALL ON accounts FROM public` ex of revoking privileges

To be able to properly set privileges you first need to know about postgreSQL
"internal organization".

# PostgreSQL architecture

PostgreSQL is made of (a) cluster(s). A cluster contains one or more databases.
A database contains one or more schemas. A schema contains tables (and views,
indexes, sequences, data types, functions, operators). 

    +----------------------+
    | cluster              |
    | |------------------| |
    | | databases        | |
    | | +--------------+ | |
    | | | schemas      | | |
    | | | +----------+ | | |
    | | | | tables   | | | |
    | | | +----------+ | | |
    | | +--------------+ | |
    | +------------------+ |
    +----------------------+ 


By default there is a schema named "PUBLIC" present in each database, everyone 
has `CREATE` and `USAGE` privileges on it.
All objects created without mentioning the schema name is added to "PUBLIC" schema.

By default, users cannot access any objects in schemas they do not own. To allow
that, the owner of the schema must grant the `USAGE` privilege on the schema.

To be able to access any object, a user first need to have access to its
containers.

For example, if we want to create the user "Alice" and give her the right to
select, insert and update data in the table `users` in schema `public` in the
database `foo`. Alice needs to be able to:

* log in 
* connect to the database `foo`
* access the element in the schema `public`
* select, insert and update the table `users`

First we (the owner) need to create a role with the `LOGIN` attribute or a user:
  
    CREATE ROLE alice LOGIN PASSWORD 'password'
    -- or
    CREATE USER alice PASSWORD 'password';

Then Alice needs to be able to connect to the database:

    GRANT CONNECT ON DATABASE foo TO alice;

Then we (the owner) need to give alice the right to access the obects of the
schema `public`:

    GRANT USAGE ON SCHEMA public TO alice;

Finally, we can give alice the permission to select, insert and update the table
`users`:

    GRANT SELECT, INSERT, UPDATE ON users TO alice;

And voilà !

I hope it makes more sense now. Bye. Take care of your dogs.

### bibliography

* <https://www.postgresql.org/docs/11/default-roles.html>
* <https://www.postgresql.org/docs/11/sql-createrole.html> 
* <https://www.postgresql.org/docs/11/database-roles.html>
* <https://www.postgresql.org/docs/11/ddl-priv.html>
* <https://www.youtube.com/watch?v=CuwsdXyBVFY>: 
* <https://www.youtube.com/watch?v=AsQUS1rWIWY>
* <https://www.postgresql.org/docs/11/ddl-schemas.html>
* <http://www.postgresqltutorial.com/postgresql-roles/>
* <https://www.postgresql.org/docs/11/sql-grant.html>
* <https://tableplus.io/blog/2018/04/postgresql-how-to-grant-access-to-users.html>
