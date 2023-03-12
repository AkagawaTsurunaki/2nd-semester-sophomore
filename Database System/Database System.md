# DATABASE SYSTEM (Northeastern University - China)

## Chapter 1: Introduction

## Chapter 2: Relational Model

### Structure of Relational Databases

#### Basic Structure

**tuple**: row

**attributes**: column, required to be atomic (indivisible).

**domain**: the set of allowed values for each attribuite. **null** is a member of every domain.

#### Relation

$r \subset D_1 \times D_2 \times \cdots \times D_n$

$r = \left ( a_1, a_2, \cdots, a_n \right ), \ a_i \in D_i$

#### Tuple Variable

$t[\text{name}]=\text{Akagawa}$

#### Relation Schema

Attribute name: $A_i$

Relation schema: $R=\left ( A_1, A_2, \cdots , A_n \right)$

Relation to the relation schema: $r(R)$

Relation instance: table

#### Relations are Unordered

Order of tuples is irrelevant (tuples may be stored in an arbitrary order)

#### Relation Database

A database consists of multiple relations.

Information about an enterprise is broken up into parts, with each relation storing one part of the information.

Storing all information as a single relation.

Normalization theory.

#### Keys

$K$ is a set of attributes, let $K \in R$

$K$ is a **superkey** of $R$ if values for $K$ are sufficient to identify a unique tuple of each possible relation $r(R)$

Superkey $K$ is a **candidate key** if $K$ is minimal (no subset of it is superkey)

**Primary key** is a candidate key chosen as the principal, means of identifying tuples `<u>`within a relation`</u>` (Should choose an attribute whose value never, or very rarely, changes.)

A relation $r1$ (referencing relation) may have an attribute that corresponds to the primary key of another relation $r2$ (referenced relation). The attribute is called a **foreign key**.

![image-20230311215343734](\Database System.assets\image-20230311215343734.png)

#### Referencing Constraint

Only values occurring in the primary key attribute of the **referenced relation** may occur in the foreign key attribute of the **referencing relation**

#### Schema Diagram

![image-20230311215617618](\Database System.assets\image-20230311215617618.png)

#### Query Languages

- **Definition**: Language in which user requests information from the database.
- **Categories of languages**: Procedural, Non-procedural, or declarative
- **“Pure” languages** - form underlying basis of query languages that people use
  - Procedural: Relational algebra
  - Non-procedural: Tuple relational calculus, Domain relational calculus

### Fundamental Relational-Algebra-Operations

#### Relational Algebra

**Definition**: Consists of a set of operators take one or two relations as inputs and produce a new relation as a result

**Six basic operators**

- **Select**: $\sigma_{p}(r)$
  - **Definition**: $\sigma_{p}(r) = \left\{ t | t \in r \and p(t) \right\}$
  - **Operation**: Select tuples that satisfy a given predicate $p$.
  - **Example**: $\sigma_{A=B \and {D>5}}(r)$

![image-20230311220742991](\Database System.assets\image-20230311220742991.png)

- **Project**: $\Pi_{A_1, A_2, \cdots, A_k}(r)$

  - **Definition**:
  - **Operation**: A unary operation, picking certain columns.

    - The result is defined as the relation of *k* columns obtained by erasing the columns that are not listed.
    - Duplicate rows removed from result, since relations are sets.
  - **Example**: $\Pi_{A,C}(r)$

![image-20230311221221638](\Database System.assets\image-20230311221221638.png)

- **Union**: $r \cup s$
  - **Definition**: $r \cup s = \left\{ t | t \in r \or t \in s \right\}$
  - **Operation**: Analogous to set union operation.
    - r, s must have the same arity (same number of attributes)
    - The attribute domains must be compatible
  - **Example**:

![image-20230311221704273](\Database System.assets\image-20230311221704273.png)

- **Set difference**: $r - s$

  - **Definition**: $r - s = \left\{ t | t \in r \and t \notin s \right\}$
  - **Operation**: Analogous to set difference operation.

    - r, s must have the same arity (same number of attributes)
    - The attribute domains of r and s must be compatible
  - **Example**:

![image-20230311222233351](\Database System.assets\image-20230311222233351.png)

- **Cartesian product**: $r \times s$

  - **Definition**: $r \times s = \left\{ tq | t \in r \and q \in s \right\}, R \cap S = \varnothing$
  - **Operation**: Pair each tuple of one relation with each tuple of another.

    - If attributes of *r(R)* and *s(S*) are not disjoint, then **renaming** must be used
  - **Example**:

![image-20230311222532221](\Database System.assets\image-20230311222532221.png)

- **Rename**: $\rho_{X}(E)$ $\rho_{X(A_1, A_2, \cdots, A_n)}(E)$
  - **Operation**
    - $\rho_{X}(E)$: Return the expression E under the name X.
    - $\rho_{X(A_1, A_2, \cdots, A_n)}(E)$: Return the result of expression E under the name X, and with the attributes renamed to $A_1, A_2, \cdots, A_n$.

#### Additional Relational-Algebra-Operations

- **Set intersection** $r \cap s$

  - **Definition**: $r \cap s = \left\{ t | t \in r \and t \in s \right\} = r - (r - s)$
  - **Operation**:

    - *r*, *s* have the *same arity*
    - attributes of *r* and *s* are compatible
  - **Example**:

![image-20230311225500984](\Database System.assets\image-20230311225500984.png)

- **Natural join** $\bowtie$

  - **Definition**: $r \cap s = \left\{ t | t \in r \and t \in s \right\} = r - (r - s)$
  - **Operation**:

    - *r*, *s* have the *same arity*
    - attributes of *r* and *s* are compatible
  - **Example**:

![image-20230311230631362](\Database System.assets\image-20230311230631362.png)

- Division $\div$

  - **Definition**:
  - **Operation**:
  - **Example**:

![image-20230311230036294](\Database System.assets\image-20230311230036294.png)

- **Assignment** $\leftarrow$

#### Extended Relational-Algebra-Operations

- **Generalized Projection** $\Pi_{F_1, F_2, \cdots, F_n}(E)$

  - **Operation**: Extends the projection operation by allowing arithmetic functions to be used in the projection list.
    - *E* is any relational-algebra expression.
    - Each of ${F_1, F_2, \cdots, F_n}$ are arithmetic expressions involving constants and attributes in the schema of *E*.
  - **Example**: $\Pi_{\text{name, money-balance}(\text{creditinfo})}$
- **Aggregate Functions** $\mathcal{G}_{F_1(A_1), F_2(A_2), \cdots, F_n(A_n)}(E)$      $_{G_1, G_2, \cdots, G_n} \mathcal{G}_{F_1(A_1), F_2(A_2), \cdots, F_n(A_n)}(E)$
  - **Operation**: Aggregate function takes a collection of values and returns a single value as a result.
    - **Some operations**: `avg`, `min`, `max`, `sum`, `count`.
    - Result of aggregation does not have a name, so we can use rename operation to give it a name. For convenience, we permit renaming `as` as part of aggregate operation. For example, $_\text{branch\_name} \mathcal{G} _\text{sum(balance) as sum-balance}  (\text{account})$
    - ![image-20230312093149317](\Database System\Database System.assets\image-20230312093149317.png)
  - **Examples**:

![image-20230312092922163](\Database System.assets\image-20230312092922163.png)

![image-20230312093218767](\Database System.assets\image-20230312093218767-16785879828311.png)

- **Outer Join** ⟕ ⟖ ⟗

  - **Operation**:

    - An extension of the join operation that avoids loss of information
    - Computes the join and then adds tuples from one relation that does not match tuples in the other relation to the result of the join
    - Uses *null* values.
  - **Examples**:

![image-20230312094212401](\Database System.assets\image-20230312094212401.png)

#### Null Values

- It is possible for tuples to have a null value, denoted by `null`, for some of their attributes
- `null` signifies an unknown value or that a value does not exist.
- The result of any arithmetic expression involving `null` is `null`
- Aggregate functions simply ignore `null` values (as in SQL)
- For duplicate elimination and grouping, `null` is treated like any other value, and two nulls are are assumed to be the same
- Comparisons with null values return the special truth value: `unknown`
- Result of select predicate is treated as `false` if it evaluates to `unknown`
- Three-valued logic using the truth value *unknown*:

  - OR

    - (*unknown* **or** *true*) = *true*
    - (*unknown* **or** *false*) = *unknown*
    - (*unknown* **or** *unknown*) *= unknown*
  - AND

    - (*true* **and** *unknown*) = unknown,
    - (*false* **and** *unknown*) = false,
    - *unknown* **and** *unknown*) *= unknown*
  - NOT

    - (**not** *unknown*) *= unknown*
  - In SQL “*P* **is unknown**” evaluates to true if predicate *P* evaluates to *unknown*

#### Modification of the Database

- Deletion $r \leftarrow r-E$
- Insertion $r \leftarrow r\cup E$
- Updating $r \leftarrow \Pi_{F_1, F_2, \cdots, F_i}(r)$

## Chapter 3: SQL

### Data Definition

#### History (Omitted)

#### Data Definition Language (Omitted)

#### Domain Types in SQL

`char(n)`: user-specified

`varchar(n)`: user-specified

`int`: machine-dependent

`smallint`: machine-dependent

`numeric(p, d)`: d digits to the right of decimal point; user specified precision of p digits.

`real, double precision`: machine-dependent

`float(n)`: user-specified

#### Create Table Construct

```sql
create table r(A_1 D_1, A_2 D_2, ..., A_N D_N,
(integrity-constraint_1),
...,
(integrity-constraint_k))
```

#### Integrity Constraints

not null

primary key (A_1, ..., A_n )

#### Drop Table Constructs

```sql
drop table r
# Deletes not only all tuples of r, but also the schema for r
```

```sql
delete table r
# Retains relation r, but deletes all tuples in r
```

#### Alter Table Constructs

```sql
alter table r add A D
# The alter table command is used to add attributes to an existing relation.
# All tuples in the relation are assigned null as the value for the new attribute.
```

```sql
alter table r drop A
# The alter table command can also be used to drop attributes of a relation.
# Dropping of attributes is not supported by many databases
```

### Basic Query Structure

#### The select clause

```sql
select distinct branch_name # To force the elimination of duplicates, insert the keyword distinct after select.
from loan
```

```sql
select all branch_name # The keyword all specifies that duplicates not be removed. Default is all
from loan
```

```sql
select * from loan
# An asterisk in the select clause denotes "all attributes"
```

```sql
select loan_number, branch_name, amount*100
from loan
# contain arithmetic expressions(+-*/)
```

#### The where clause

The where clause specifies conditions that the result must satisfy.

Logical connectives: `and`, `or`, `not`

Comparison operation: `<`, `>`, `<=`, `>=`, `==`, `<>`.

#### The from clause

The from clause lists the relations involved in the query.

#### The Rename Operation

```sql
old-name as new-name
```

#### String Operations

```sql
select customer_name
from customer
where customer_street like '% Main_%' 
# The % character matches any substring that have any length (can be 0).
# The _ character matches any character.
```

- SQL supports a variety of string operations such as

  - concatenation (using “||”)

  - converting from upper to lower case (and vice versa)

  - finding string length, extracting substrings, etc.

#### Ordering the Display of Tuples

```sql
select *
from loan
order by amount desc, loan_number asc
# For each attribute, ascending order is the default
```

#### Duplicates

```sql
select A_1, A_2, ..., A_n
from r_1, r_2, ..., r_m
where P;
```

$\Pi_{A_1, A_2, \cdots, A_n} \left( \sigma_P (r_1 \times r_2 \times \cdots \times r_m) \right)$

### Set Operations

- The set operations `union`, `intersect`, and `except` operate on relations and correspond to the relational algebra operations $\cup, \cap, -$.
- Each of the above operations automatically eliminates duplicates.
- To retain all duplicates use the corresponding multiset versions `union all`, `intersect all` and `except all`.

### Aggregate Functions

Operations: `avg`, `min`, `max`, `sum`, `count`.

```sql
select branch_name, count (distinct customer_name)
from depositor, account
where depositor.account_number = account.account_number
group by branch_name
# Attributes in select clause outside of aggregate functions must appear in group by list
```

```sql
select branch_name, avg (balance)
from account
group by branch_name
having avg (balance) > 1200
# Predicates in the having clause are applied after the formation of groups whereas predicates in the where clause are applied before forming groups
```

### Null Values

### Nested Subqueries

### Complex Queries 

### Views

### Modification of the Database

### Joined Relations** 


