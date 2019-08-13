---
layout: post
title: "What is SQL Injection"
date: 2019-08-15
image: whatIsSQLInjection.jpg
category: tutorials

---

# What is SQL
SQL or Structured Querry Language is a language used in programming, designed for accessing and manipulating relational databases.

# What is SQL injection
SQL inection attack consists of "injection" of a SQL querry via the input data from the client to the application. Successful SQL injections can Insert, Update, Delete or Read data from the associated database. In some cases even administration operations are possible e.g. shutdown the DBMS or can issue commands to the operating system.

# Types of SQL injections

There are two common main types of SQL injections - Classic and Blind SQL injections

## Classic SQL injections
This is the most easy-to-exploit type of SQL injection. It occurs when the attacker is able to use the same communication channel to launch the attack and gather the results. There are two common classic examples of Classic SQL injections - Error-based and Union-based

### Error-based
Error based relies on error messages returned by the database server to obtain information about the structure of the querry and the server. There are cases, where the attacker can get enough information to enumerate an entire database.

### Union-based
Union-based injections leverages the UNION operator to combine the results of SELECT statements into a single result.

## Blind SQL injection
In the blind SQL injections, no data is transferred via the web application and the attacker is not able to see the result of an attack. There are two common types of Blind SQL injections - Boolean-based and Time-based

### Boolean-based
Boolean-based SQL injection is a technique that relies on sending SQL query to the application, forcing it to return different result depending on whether the query returns TRUE or FALSE. Depending on the result, the attacker observes the content within the HTTP response and gets to know if the payload returned true or false, even though no data from the DB is returned

### Time-based
Time-based SQL injection is a technique that relies on sending SQL query which forces the DB to wait for a specified amount of time before responding.

# Examples

## Classic SQL Injection

If we have the following query

```
SELECT * FROM Users WHERE Username='$username' AND Password='$password'
```
If we fill the form such way:

```
$username = 1' or '1' = '1'
$password = 1' or '1' = '1'
```
The querry will be filled like:

```
SELECT * FROM Users WHERE Username='1' OR '1' = '1' AND Password='1' OR '1' = '1' 
```
This will result in the query returning true, because `OR '1' = '1'`. in Such case the query will return all the users, and their passwords

## Union SQL Injection

If we have the following query

```
SELECT Name, Phone, Address FROM Users WHERE Id=$id
```
And we set the value $id to

```
$id=1 UNION ALL SELECT creditCardNumber,1,1 FROM CreditCardTable
```

Will result in the following querry

```
SELECT Name, Phone, Address FROM Users WHERE Id=1 UNION ALL SELECT creditCardNumber,1,1 FROM CreditCardTable
```
Which will join the result of the original query with all the credit card numbers in the CreditCardTable table. The keyword ALL is necessary to get around queries that use the keyword DISTINCT. Moreover, we notice that beyond the credit card numbers, we have selected two other values. These two values are necessary because the two queries must have an equal number of parameters/columns in order to avoid a syntax error