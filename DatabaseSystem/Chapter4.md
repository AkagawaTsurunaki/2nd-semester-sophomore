# Chapter 4: Advanced SQL

## SQL Data Types and Schemas

### Built-in Data Types in SQL

`date`: Made up of **year-month-day** in the format `yyyy-mm-dd`, e.g.`‘2005-07-27’`

`time`: Made up of **hour:minute:second** in the format `hh:mm:ss`, e.g.`‘09:00:30’`

`time(i)`: Made up of **hour:minute:second:ii...i** in the format `hh:mm:ss:ii...i`, e.g.`‘09:00:30.75’`

`timestamp`: date plus time of day

`interval`: period of time

- Subtracting a date/time/timestamp value from another gives an interval value

- Interval values can be added to date/time/timestamp values

`extract (year from r.starttime) `: Can extract values of individual fields from date/time/timestamp.

`cast <string-valued-expression> as date`: Can cast string types to date/time/timestamp

### User-Defined Types

#### Create user-defined type

```sql
create type Dollars as numeric (12,2) final 
```

#### create user-defined domain 

```sql
create domain person_name char(20) not null
```

### Domain Constraints

#### Goal

Ensure that the comparisons make sense.

#### Example

```sql
create domain Dollars numeric(12, 2)
create domain Pounds numeric(12,2)
(cast r.A as Pounds * 0.911)
```

### Large-Object Types

#### **blob**

Binary large object, uninterpreted for database.

#### **clob**

Character large object  

## Integrity Constraints 

Integrity constraints guard against accidental damage to the database, by ensuring that authorized changes to the database do not result in a loss of data consistency.

### Constraints on a Single Relation

#### `not nul`l

#### `primary key`

#### `unique(A1, A2, …, Am)`

The unique specification states that the attributes $A_1, A_2, … A_m$ form a candidate key.
Candidate keys are permitted to be null (in contrast to primary keys).

#### `check (P)`

where P is a predicate, permits domains to be restricted

```sql
# Declare branch_name as the primary key for branch and ensure that the values of assets are non-negative.
create table branch(
     branch_name	char(15),
     branch_city	char(30),
     assets			integer,
     primary key (branch_name),
     check (assets >= 0)
)
```

```sql
# The domain has a constraint that ensures that the hourly_wage is greater than 4.00
create domain hourly_wage numeric(5,2) constraint value_test check(value > = 4.00)
# The clause constraint value_test is optional; useful to indicate which constraint an update violated.
```

### Referential Integrity

- Ensures that a value that appears in one relation for a given set of attributes also appears for a certain set of attributes in another relation.

- Primary and candidate keys and foreign keys can be specified as part of the SQL create table statement.

- The `primary key` clause lists attributes that comprise the primary key.

  - ```sql
    create table customer(
        customer_name	char(20),
        customer_street	char(30),
        customer_city	char(30),
        primary key (customer_name)
    )
    ```

- The `unique` clause lists attributes that comprise a candidate key.

- The `foreign key` clause lists the attributes that comprise the foreign key and the name of the relation referenced by the foreign key. 

  - By default, a foreign key references the primary key attributes of the referenced table.

  - ```sql
    create table account(
        account_number	char(10),
        branch_name		char(15),
        balance	         integer,
        primary key (account_number), 
        foreign key (branch_name) references branch 
    )
    ```

### Assertions

#### Form

```sql
create assertion <assertion-name> check <predicate>
```

```sql
not exists X such that not P(X)
```

#### Example

```sql
# The sum of all loan amounts for each branch must be less than the sum of all account balances at the branch.
create assertion sum_constraint check (
  not exists (
      	select *
		from branch
    	where (
			select sum(amount)
           	from loan
			where loan.branch_name = branch.branch_name 
        ) >= (
        select sum(balance) 
        from account
		where account.branch_name = branch.branch_name
        )
  )
)
```

## Authorization

### Forms of authorization on parts of the database

**Read**: allows reading, but not modification of data.
**Insert**: allows insertion of new data, but not modification of existing data.
**Update**: allows modification, but not deletion of data.
**Delete**: allows deletion of data.

### Forms of authorization to modify the database schema (covered in Chapter 8):

**Index**: allows creation and deletion of indices.
**Resources**: allows creation of new relations.
**Alteration**: allows addition or deletion of attributes in a relation.
**Drop**: allows deletion of relations.

### Authorization Specification in SQL

#### Functionality

- The grant statement is used to confer authorization.
- Granting a privilege on a view does not imply granting any privileges on the underlying relations.
- The grantor of the privilege must already hold the privilege on the specified item (or be the database administrator).

#### Form

```sql
grant <privilege list> # A list of Privileges All privilege, all allowable privileges
on <relation name or view name> to <user list> # A list of user-id public, all current and future users of the system.
```

### Privileges in SQL

**select**: allows read access to relation, or the ability to query using the view

```sql
grant select on branch to U1, U2, U3
```

**insert**: the ability to insert tuples
**update**: the ability  to update using the SQL update statement
**delete**: the ability to delete tuples.
**all privileges**: used as a short form for all the allowable privileges

### Revoking Authorization in SQL

#### Functionality 

- The revoke statement is used to revoke authorization.
- If the same privilege was granted twice to the same user by different grantees, the user may retain the privilege after the revocation.
- All privileges that depend on the privilege being revoked are also revoked

#### Form

```sql
revoke <privilege list>
on <relation name or view name> 
from <user list>
```

## Embedded SQL

## Dynamic SQL

## ODBC and JDBC