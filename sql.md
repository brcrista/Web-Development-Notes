## Why use Entity Framework?
I thought it would be educational to use ADO.NET, write my own SQL and translate the results to .NET types.

After trying out Entity Framework, it has a lot of advantages.
1. **Frameworks exist to protect you against problems you didn't know you had.**  Entity Framework will automatically handle resiliency issues such as retries.
2. **Higher-level programming model.**
    a. You don't need to write your own SQL, and you don't need to write your own intermediate types between your object model and the SQL layer.
    b. Also, reading the raw SQL results is error-prone boilerplate.  For example, you need to use `long` instead of `int` for IDs, and you need to remember to use `DBNull` instead of `null`.
    c. Entity Framework also lets you put foreign-key references right on the model types that get filled in automatically.  You can even put references going in the other direction relative to SQL for one-to-many relationship.
    d. In sum, Entity Framework lets you start with your .NET data model and writes SQL around that, not the other way around.
3. **Generate migrations automatically.**  Otherwise, you're stuck writing upgrade SQL scripts by hand.

## Why use VSSF and custom sprocs?
VSSF doesn't use ADO or Entity Framework.  Rather, it is built around a `ResultSet` type, sprocs to get data from the database, and `Component` types that translate `ResultSet` to the object model.

The reasons for sprocs as opposed to dynamically-generated SQL are:
* Predictable query plans
* Greater control over query plans
* Query plan reuse through caching
* All data access code confined to a single layer
* Sprocs are versioned and upgraded with the schema

## `rowversion`

In the VSSF SQL guidelines, we say not to use `rowversion` as "a watermark to determine which rows are new." It cites an incident where one table was tracking `rowversion` from another table to know when to delete rows. The data in the upstream table was migrated to a new table, which reset `rowversion` in all of its rows. Then, the cleanup job ran on the downstream table and deleted all its rows.

What you *can* use `rowversion` for is to detect concurrency conflicts, as in <https://docs.microsoft.com/en-us/aspnet/core/data/ef-mvc/concurrency?view=aspnetcore-3.1#detecting-concurrency-conflicts>.
