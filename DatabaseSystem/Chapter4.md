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

Ensures that a value that appears in one relation for a given set of attributes also appears for a certain set of attributes in another relation.

## Authorization

## Embedded SQL

## Dynamic SQL

## ODBC and JDBC