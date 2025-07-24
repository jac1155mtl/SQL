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
N/A

### 1.3.2 THE HIERARCHICAL DATABASE MODEL
IMS was the first hierarchical database developed and is still in use today because IBM has continually upgraded it.

> Defn. The *hierarchical database model* organizes data into levels, where each level contains a single category of data, and parent-chield relationships between levels. Each parent item can have multiple children, but each child item can have one and only one parent.

Three relationships can occur between objects in a database:
- **One-to-one relationship:** one object of the first type is related to one and only one object of the second type.
- **One-to-many relationship:** one object of the first type is related to multiple objects of the second type.
- **Many-to-many relationship:** multiple objects of the first type are related to multiple objects of the second type.

Many-to-many relatioships are not handled cleanly in hierarchical databases.

A great strength of the hierarchical model is its high performance. Because relationships between entitities are simple and direct, retrievals from a hierarchical database are set up to take advantages of the way the data is structured can be very fast. 

It's difficult to change the structure of a hierarchical database to address new requirements. This structural rigidity is the greatest weakness of the hierarchical model. Another problem with the hierarchical model is that it requires a lot of redundancy[^1].

Even more damaging than the wasted  space from redundant data is the possibility of data corruption. Whenever multiple copies of the same data exist in a database, there is the potential for modification anomalies.

> Defn. *Modification anomaly* is an inconsistency in the data after a modification is made.

[^1]: see Fig. 1-01 and 1-02.

### 1.3.3 THE NETWORK DATABASE MODEL
A year after IMS was first run, the network database model was described. 

The designers of the *network model* opted for an architecture that does not duplicate items, but instead increases the number of relationships associated with some items[^2].

[^2]: see Fig. 1-03.

### 1.3.4 THE RELATIONAL DATABASE MODEL
In 1970, a year after the network database model, Dr. Edgar F. "Ted" Codd, also at IBM, [published a paper](https://dl.acm.org/doi/10.1145/362384.362685) introducing the *relational database* model. 

It clearly had an advantage over the hierarchical model in that data redundancy was minimal; it had an advantage over the network model with its relatively simple relationships. Due to the complexity of the relational databse engine that it required, any implementation would be much slower than a comparable implentation of either the hierarchical or the network model. It was almost ten years before the first implementation of the relational model.

#### Defining what makes a database relational

The original definition: 
> Defn. A *relational database* must consist of two-dimensional tables of rows and columns, wher the cell at the intersection of a row and column contains an atomic value.

Each row in a table must be uniquely identifiable -- every table in a relational databse must have a *primary key*[^3].

[^3]: see Fig. 1-04.

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

mind Databases structured according to the heirarchical and network models had excellent performance, they were difficult to maintain. 

The performance improvements in processors, memories and hard disk combined to dramatically improve the performance of relational database systems, making them more competitive with hierarchical and network systems.

# CHAPTER 2 MODELING A SYSTEM
SQL is the language that you use to create and operate on relational databases. Before you can do that database creation, you must first create a conceptual model for the system to built. In order to develop a database system that delivers the results, performance and reliability that the users need, you must understand in a highly detailed way what those need are. 

After perfecting the model through much dialog with the user, you need to translate the model into something that can be implemented with a relational database.

## 2.1 CAPTURING THE USERS' DATA MODEL
the whole purpose of a database is to hold useful data and enable one or more people to selectively retrieve and use the data they want. more often than not, people's ideas of what should be included in the database and what they want to get out of it are not terribly precise. the concepts each interested party may have in mind comes from their own data models. when all those data models from various users are combined, they become one (huge) data model.

to build a database system that meets the needs of the users, you must understand this collective data model.

beyond understanding the data model, you must help clarify it so that it can become the basis for a useful database system. 

### 2.1.1 IDENTIFYING AND INTERVIEWING STAKEHOLDERS
the first step in discovering the users' data model is to find out who the users are. 

identifying the database users goes beyond the people who actually sit in front of a PC and run your database application. you need to find these people, interview them, and find out how they envision the system. try to gain as complete an understanding of the current situation as possible:

- if the functions to be performed by the new system are already being performed, by either a manual system or an obsolete computerized system, explain how the current system works?
- what do the users like about the current system?
- what do the users not like about the current system?
- what is the motivation for moving to a new system?
- what desirable features are missing from what they have now?
- what annoying aspects of the current system are frustrating them?

### 2.1.2 RECONCILING CONFLICTING REQUIREMENTS
as the set of stakeholders will be diverse, so will their ideas of what the system should be and do. if such ideas are not reconciled, you run the risk of developing a system that is not satisfactory to anybody.

it is your responsibility as the database developer to develop a consensus. as part of your responsiblity, you need to separate the stated requirement of the stakeholders into three categories:
- **mandatory:** a feature that is absolutely essential. the system would be of limited value without it
- **significiant:** a feature that is important and that adds greatly to the value of the system
- **optional:** a feature that would be nice to have, but is not actually needed.

you need to convince all the stakeholders that their cherished features that fall into the optional category must be deleted or changed if they conflit with someone else’s mandatory or significant feature. also, some stakeholders have more clout than others. you must be sensitive to this.

### 2.1.3 OBTAINING STAKEHOLDER BUY-IN
one way or another, you will have to convince all the stakeholders to agree on one set of features that will be included in the system you are planning to build. get it in writing. enumerate everything that will be provided in a formal Statement of Requirements, and then have every stakeholder sign off on it.

## 2.2 TRANSLATING THE USERS' DATA MODEL TO A FORMAL ENTITY-RELATIONSHIP MODEL
after you outline a coherent users’ data model in a clear, concise, concrete form, the real work begins. you must transform that model into a relational model that serves as the basis for a database. a helpful technique is to first translate it into one of several formal modeling systems that clarify the various entities in the users’ model and the relationships between them. probably the most popular of these formal modeling techniques is the Entity-Relationship (ER) model.

in order to design a relational database properly, you must have a good understanding of database structure.
  
### 2.2.1 ENTITY-RELATIONSHIP MODELING TECHNIQUES
in 1976, six years after Dr. Codd published the relational model, Dr. Peter Chen [published a paper](https://dl.acm.org/doi/10.1145/320434.320440) introducing the ER model. 

>N.B. The ER model was an important factor in turning theory into practice because one of the strengths of the ER model is its generality. 

Any ER model, big or small, consists of four major components: entities, attributes, identifiers, and relationships.

#### Entities
>Defn. an *entity* is something that the user can identify and that they want to keep track of. a group of entities with common characteristics is called an *entity class*. any one example of an entity class is an *entity instance*.

#### Attributes
>Defn. aspects of an entity are referred to as *attributes*.

#### Identifiers
in order to do anything with data, you must be able to distinguish one piece of data from another. that means each piece of data must have an identifying characteristic that is unique. in the context of a relational database, a “piece of data” is a row in a two-dimensional table. 

|ER Model       |Relational Database|
|:---:          |:---:              |
|Entity Class   |Table              |
|Entity Instance|Row                |
|Attribute      |Column             | 

nonunique identifiers are also possible.

another way, however is to use a *composite identifier* which is a combination of several attributes that together are sufficient to uniquely identify a record.

#### Relationships 
any nontrivial relational database contain more than one table. when you have more than one table, the question arises as to how the tables relate to each other. relationships can differ in the number of entities that they relate.

##### Degree-Two Relationships
>Defn. *degree-two relationships* are ones that relate one entity directly to one other entity. degree-two relationships are also called *binary* relationships[^4].

[^4]: see Fig. 2-03.

degree-two relationships are the simplest possible relationships and just about any system that you likely want to model consists of entities connected by degree-two relationships, although more complex relationships are possible.

there three kinds of binary relationships:
- **One-to-one (1:1) relationship:** relates one instance of one entity class to one instance of a second entity class
- **One-to-many (1:N) relationship:** relates one instance of one entity class to multiple instances of a second entity class
- **Many-to-many (N:M) relationship:** relates multiple instances of one entity class to multiple instances of a second entity class

many-to-many relationships can be very confusing are not well represented by the two-dimensional table architecture of a relational database. consequently, such relationships are almost always converted to simpler one-to-many relationships before they are used to build a database

##### Complex Relationships
*degree-three* relationships are possible, but rarely occur in practice. relationships of degree higher that three probably mean you need to redesign your system to use simpler relationships.

>Tip. altough it is possible to build a system with such relationships, it is probably better in most cases to restructure the system in terms of binary relationships.

### 2.2.2 DRAWING ENTITY-RELATIONSHIP DIAGRAMS
>Defn. systems represented by the ER model are unversally depicted in the form of diagrams. these are called *ER diagrams*.

>Defn. for ER models, *cardinality* is the number of entity instances in a entity class.

In the context of relational databases, a relationship between two tables has two cardinalities of interest: the cardinalities of the two tables. we look at these two cardinalities in two primary ways: maximum cardinality and mimimum cardinality.

##### Maximum Cardinality
>Defn. the *maximum cardinality* of one side of a relationship shows the largest number of entity instances **that can be** on that side of the relationship.

##### Minimum Cardinality
>Defn. the *minimum cardinality* shows the least number of entity instances that can be on that side of the relationship. 

in some cases, the least number of entity instances that can be on one side of a relationship can be zero. in other cases, the minimum cardinality could be one or more.

in an ER diagram, the slash mark on the side of an entity class denotes a mimimum cardinaly of *mandatory*, meaning at least one instance must exist. the oval on the side of an entity class denotes a mimium cardinality of *optional*[^5].

[^5]: see Fig. 2-08. 

>N.B. minimum cardinality is often difficult to determine. you’ll need to question the users very carefully and explore unusual cases before deciding how to model minimum cardinality.

if the minimum cardinality of one side of a relationship is mandatory, that means the cardinality of that side is at least one, but might be more.

>Tip. primarily, you are interested in whether the minimum cardinality on a side of a relationship is either mandatory or optional and less interested in whether a mandatory minimum cardinality has a value of one or more than one. the difference between mandatory and optional is the difference between an entity exists or not.

### 2.2.3 UNDERSTANDING ADVANCED ER MODEL CONCEPTS
subtle differences in the way users model their system can modify the way minimum cardinality is modeled.

more complex situations are bound to arise.

##### Strong Entities and Weak Entities
all entities are not created equal. 

>Defn. an entity that does not depend on any other entity for its existence is considered a *strong entity*

strong entities are represented in ER diagrams as rectangles with sharp corners.

>Defn. any entity that is existense-dependent on another entity is a *weak entity*.

in an ER diagram, a weak entity is represented with a box that has rounded corners. the diamond that shows the relationship between a weak entity and its corresponding strong entity also has rounded corners.[^6].

[^6]: see Fig. 2-11.

##### ID-Dependent Entities
>Defn. a special case of a weak entity is one that depends on a strong entity not only for its existence, but also for its identity. this is called an *ID-dependent entity*.

##### Supertype and subtype entities
in some databases, you may find some entity classes that might actually share attributes with other entity classes. 

Supertype/subtype relationships borrow the concept of *inheritance* from object-oriented programming. the attributes of the *supertype entity* are inherited by the subtype entities. each *subtype entity* has additional attributes that it does not necessarily share with the other subtype entities.

in an ER diagram, the `$\epsilon$` next to each relationship line signifies that the lower entity is a subtype of the higher entity. the curved arc with a number 1 at the right represents the fact that every member of supertype entity must be a member of one of the subtypes entities. it is possible in some models that an element could be a member of a supertype without being a member of any of the subtypes[^7].

[^7]: see Fig. 2-13.

the supertype and subtypes entities in the ER model correspond to supertables and subtables in a relational database. A supertable can have multiple subtables and a subtable can have multiple supertables. the relationship between a supertable and a subtable is always one-to-one.

##### Incorporating Business Rules
sometimes you may not find important business rules written down anywhere. they may just be things that everyone in the organization understands. it is important to conduct an in-depth interview of everyone involved to fish out any business rules that people failed to mention when the job of creating the database was first described to you.

### 2.2.4 A SIMPLE EXAMPLE OF AN ER MODEL
N/A

### 2.2.5 A SLIGHTLY MORE COMPLEX EXAMPLE
N/A

### 2.2.6 PROBLEMS WITH COMPLEX RELATIONSHIPS
it is common practice to convert a many-to-many relationship into two one-to-many relationships, both connected to a new entity that lies between the original two. you can make that conversion with no loss of accuracy and the problem of how to store things disappears. 

### 2.2.7 SIMPLIFLYING RELATIONSHIPS USING NORMALIZATION
even after you elimate all the many-to-many relationships in an ER model, there can still be problems if you have not conceptualized your entities in the simplest way. the next step in the design procress is to examine your model and see if adding, changing or deleting data can cause incosistencies or even outright wrong information to be retained in your database. such problems are called *anomalies*. this process of model adjustment is called *normalization*.

### 2.2.8 TRANSLATING AN ER MODEL INTO A RELATIONAL MODEL
after you’re satisfied that your ER model is not only correct but economical and robust, the next step is to translate it into a relational model. the relational model is the basis for all relational DBMS.