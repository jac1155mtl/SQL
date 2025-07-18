# CHAPTER 1 UNDERSTANDING RELATIONAL DATABASES
SQL is the international standard language used in conjuction with relational databases. Relational databases are the dominant form of data storage throught the world.

Different data storage strategies have been used over the eyars, each having their own strengths and weaknesses. The strengths of the relational model overshadows its weaknesses.

## 1.1 UNDERSTANDING WHY TODAY'S DATABASES ARE BETTER THAN EARLY DATABASES
Vannervar Bush conceived the idea of a database in 1945, even before the first electronic computer was built. Practical implementations of databases did not appear for a number of years after that.

### 1.1.1 IRREDUCIBLE COMPLEXITY
Any software system that performs a useful function is complex. Any nontrivial computer application has two major components: the program and the data. Developers have some control over the location of the complexity, in the program or the data part.

### 1.1.2 MANAGING DATA WITH COMPLICATED PROGRAMS
In the earliest applications of computers to problems, all the complexity resided in the program. The data consisted of one data record of fixed length after another, stored sequentially in a file. This is called a *flat file* data structure.

> Defn. *flat file* data structure: one data record of fixed length after another, stored sequentially in a file.

An example of data organized in a flat file structure: 
```
Harold Percival 26262 S. Howard Mill Road, Westminster CA92683
Jerry Appel 32323 S. River Lane Road Santa Ana CA92705
Adrian Hansen 232 Glenwood Court Anaheim CA92640 
...
```

|Advantages|Disadvantages|
|----------|-------------|
|**Storage requirements are minimized.** In the early days of electronic computers, storage was relatively expensive, so system designers were highly motivated to accomplish their tasks using as little space as possible.|**Updating the data's structure can be a huge task.** If the metadata about the structure of the data is in the program rather than the data itself, all the programs that have access that data must be modified whenever the data structure is changed.|
|**Operations on the data can be fast.** The program interacts directly with the data, no database management system (DBMS) in the middle.|**Flat file systems provide no protection of individual data elements.**|
||**Speed can be compromised.** Accessing records in a large flat file can actually be slower than a similar access in a database because flat file systems do not support indexing.|
||**Portability becomes an issue,** When hardware becomes obsolete and the system must be migrated. All the applications will have to be changed to reflect the new way of accessing the data.| 

### 1.1.3 MANAGING DATA WITH SIMPLE PROGRAMS

The major selling point of database systems is that the metadata resides on the data end of the system rather than the program. The program makes *logical* requests for data and the DBMS translates those logial requests into commands that go out to the physical storage hardware. 

> Defn. *logical* request: asking for a specific piece of information, but not specifying the location on the hard disk.

|Advantages|Disadvantages|
|----------|-------------|
|Programs are unaffected when the physical details of where the data is stored changes.|Placing a DBMS in between the application program and the data slows down operations on that data.|
|Portability across platforms is easy as long as the DBMS used by the first platform is also available on the second. Generally, you don't need to change the programs at all to accomodate various platforms.|Databases take up more space on disk storage than the same amount of data would take up in a flat file system. This is due to the fact that metadata is stored along with data.|

### 1.1.4 WHICH TYPE OF ORGANIZATION IS BETTER?
The answer is not quite so simple. To change to a more modern database system requires rewriting all applications from scratch and reorganizing all the data. As a result, legacy flat file systems continue to exist because switching isn't feasible. 

## 1.2 DATABASES, QUERIES AND DABATASE APPLICATIONS
A flat file system is not really very much like a haystack, but it does lack structure - in order to find a particular record in such a file, you must use tools that lie outside of the file itself.

### 1.2.1 MAKING DATA USEFUL
For a collection of data to be useful, you must be able to easily and quickly retrieve the particular data you want. One way to make this happen is to store the data in a logical structure. 

### 1.2.2 RETRIEVING THE DATA YOU WANT - AND ONLY THE DATA YOU WANT
There are four types of operations that people perform on a collection of data:
- Data entry is done only once
- Changes to exisiting data are made relatively infrequently
- Data is deleted only once
- Retrieval of data is performed frequently and often repeated

If you could optimize only one operation performed on a collection of data, that one operation should be data retrieval. Modern DBMSs put a great deal of effor into making retrievals fast. 

Retrievals are performed by queries. A modern DBMS analyzes a query that is presented to it and decides how best to perform it.

> THE FIRST DATABASE SYSTEM
> ---
> The first true database system IMS (Information Management System) was developed by IBM in the 1960s in support of NASA's Apollo moon landing program. Flat file systems were out of the question.

## 1.3 EXAMINING COMPETING DATABASE MODELS

> Defn. A *database model* is a way of organizing data elements within a database.

The three database models that appeared on the scene:
- **Hierarchical:** organizes data into levels, where each level contains a single category of data, and parent-chield relationships between levels
- **Network:** organizes data in a way that avoids much of the redundancy inherent in the hierarchical model
- **Relational**: organizes data in a structured collection fo two-dimensional tables

Scientist have continued to develop database models that have been found useful in some categories of applications.

### 1.3.1 LOOKING AT THE HISTORICAL BACKGROUND OF THE COMPETING MODELS

### 1.3.2 THE HIERARCHICAL DATABASE MODEL
IMS was the first hierarchical database developed and is still in use today because IBM has continually upgraded it.

> Defn. The *hierarchical database model* organizes data into levels, where each level contains a single category of data, and parent-chield relationships between levels. Each parent item can have multiple children, but each child item can have one and only one parent.

Three realtionships can occur between objects in a database:
- **One-to-one relationship:** one object of the first type is related to one and only one object of the second type.
- **One-to-many relationship:** one object of the first type is related to multiple objects of the second type.
- **Many-to-many relationship:** multiple objects of the first type are related to multiple objects of the second type.

Many-to-many relatioships are not handled cleanly in hierarchical databases.

A great strength of the hierarchical model is its high performance. Because relationships between entitities are simple and direct, retrievals from a hierarchical database are set up to take advantages of the way the data is structured can be very fast. 

It's difficult to change the structure of a hierarchical database to address new requirements. This structural rigidity is the greatest weakness of the hierarchical model. Another problem with the hierarchical model is that it requires a lot of redundancy[^1].

Even more damaging than the wasted  space from redundant data is the possibility of data corruption. Whenever multiple copies of the same data exist in a database, there is the potential for modification anomalies.

> Defn. *Modification anomaly* is an inconsistency in the data after a modification is made.

[^1]: see Figure 1-1 and 1-2 in the book/handwritten notes.

### 1.3.3 THE NETWORK DATABASE MODEL
A year after IMS was first run, the network database model was described. 

The designers of the *network model* opted for an architecture that does not duplicate items, but instead increases the number of relationships associated with some items[^2].

[^2]: see Figure 1-3 in the book/handwritten notes.

### 1.3.4 THE RELATIONAL DATABASE MODEL
In 1970, a year after the network database model, Dr. Edgar F. "Ted" Codd, also at IBM, [published a paper](https://dl.acm.org/doi/10.1145/362384.362685) introducing the *relational database* model. 

It clearly had an advantage over the hierarchical model in that data redundancy was minimal; it had an advantage over the network model with its relatively simple relationships. Due to the complexity of the relational databse engine that it required, any implementation would be much slower than a comparable implentation of either the hierarchical or the network model. It was almost ten years before the first implementation of the relational model.

#### Defining what makes a database relational

The original definition: 
> Defn. A *relational database* must consist of two-dimensional tables of rows and columns, wher the cell at the intersection of a row and column contains an atomic value.

Each row in a table must be uniquely identifiable -- every table in a relational databse must have a *primary key*[^3].

[^3]: see Figure 1-4 in the book/handwritten notes.

The idea of separating closely related things from more distantly related things by dividing things up into tables was one the main factors distinguishing the relational model from the hierarchical and network models.

#### Protecting the definition of relational databased with Codd's rules

To fight the dilution of his model, Codd formulated 12 rules that served as criteria for determining     whether a database product was in fact relational.

1. **The information rule:** data can be represented only one way, as values in columns positions within rows of a table.
2. **The guaranteed access rule:** every value in a database must be accessible by specifying a table name, a column name and row. The row is specified by the value of the primary key.
3. **Systematic treatment of null values:** missing data is distinct from specific values, such as zero or an empty string.
4. **Relational online catalog:** authorized users must be able to access the database's structure (its *catalog*) using the same query language they use to access the database's data.
5. **The comprehensive data sublanguage rule:** the system must support at least one relational language that can be used both interactively and within application programs, that supports data definition, data manipulation, and data control functions. Today that one language is SQL.
6. **The view updating rule:** all views that are theoretically updatable must be updatable by the system.
7. **The system must support set-at-a-time insert, update, and delete operations:** this means that the system must be able to perform insertions, updates and deletions of multiple rows in a single operation.
8. **Physical data independence:** changes to the way data is stored must not affect the application.
9. **Logical data independence:** changes to the tables must not affect the application.
10. **Integrity independence:** integrity constraints must be specified independently from the application programs and stored in the catalog.
11. **Distribution independence:** distribution of portions of the database to various locations should not change the way applications function.
12. **The nonsubversion rule:** if the system provides a record-at-a-time interface, it should not be possible to use it to subvert the relational security or integrity constraints.

Over and above the original rules, in 1990, Codd added one more rule:

**Rule Zero:** for any system that is advertised as, or is claimed to be, a relational database management system, that system must be able to manage databases entirely through its relational capabilities, no matter what additional capabilities the system may support.

#### Highlighting the relational database model's inherent flexibility
The architecture of a relational database is such that it is much easier to restructure a relational database than it is to restructure either a hierarchical or network database. 

### 1.3.5 THE OBJECT-ORIENTED DATABASE MODEL
> Defn. The *object-oriented database model* accommodates the storage of types of data that don't easily fit into the categories handled by relational databases.

The object-oriented database management systems (OODBMS) were developed primarily to handle nontext, nonnumeric data such as graphical objects. A relational DBMS typically doesn't do a good job with such (so-called complex) data types. An OODBMS uses the same data model as object-oriented programming languages (e.g. Java, C++ and C\#) and works well with such languages.

### 1.3.6 THE OBJECT-RELATIONAL DATABASE MODEL
> Defn. The *object-relational model* is a merger of the relational and object models, and it is designed to capture the strengths of both, while leaving behind their major weaknesses.

An object-relational database is a relational database that allows user to create and use new data types that are not part of the standard set of data types provided by SQL. These new types were added to the SQL:1999 specification.

Current relational DBMSs are actually object-relational DMBS rather than pure relational DMBSs.

### 1.3.7 THE NONRELATIONAL NOSQL MODEL
The NoSQL model stores data as documents, instead of tables. It is designed to work with data that is not rigidly structured. 

This model is particularly appropriate for large systems consisting of clusters of servers. Because the NoSQL model stores all related data in the same document, queries for large amounts of data can be quicker than in traditional databases.

## 1.4 WHY THE RELATIONAL MODEL WON

- The earliest implementation of relational DBMSs were slow performers.
- Most business managers were reluctant to try something new when they were already familiar with one or the other of the older technologies.
- Data and applications that already existed for an existing database system would be very difficult to convert to work with a relational DBMS.
- Employees would have to learn an entirely new way of dealing with data.

Databases structured according to the heirarchical and network models had excellent performance, they were difficult to maintain. 

The performance improvements in processors, memories and hard disk combined to dramatically improve the perfo∏rmance of relational database systems, making them more competitive with hierarchical and network systems.