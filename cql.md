**CQL Stands for Cypher Query Language. Like Oracle Database has query language SQL, Neo4j has CQL as query language.**

######Neo4j CQL Commands/Clauses
The following are frequently used Neo4j CQL Commands/Clauses:

|S.No.	|CQL Command/Clause	|Usage|
|---|---|---|
|1.	|CREATE	|To create nodes, relationships and properties|
|2.	|MATCH	|To retrieve data about nodes, relationships and properties|
|3.	|RETURN	|To return query results|
|4.	|WHERE	|To provide conditions to filter retrieval data|
|5.	|DELETE	|To delete nodes and relationships|
|6.	|REMOVE	|To delete properties of nodes and relationships|
|7.	|ORDER |BY	To sort retrieval data|
|8.	|SET	|To add or update labels|

######Neo4j CQL Data Types
These data types are similar to Java language. They are used to define properties of a node or a relationship

Neo4j CQL supports the following data types:

|S.No.	|CQL Data Type	|Usage|
|---|---|---|
|1.	|boolean	|It is used to represent boolean literals: true, false.|
|2.	|byte	It |is used to represent 8-bit integers.|
|3.	|short	|It is used to represent 16-bit integers.|
|4.	|int	|It is used to represent 32-bit integers.|
|5.	|long	|It is used to represent 64-bit integers.|
|6.	|float	|It is used to represent 32-bit floating-point numbers.|
|7.	|double	|It is used to represent 64-bit floating-point numbers.|
|8.	|char	|It is used to represent 16-bit characters.|
|9.	|String	|It is used represent Strings.|

####Neo4j CQL CREATE

CREATE is the cmd to insert record in database.
 
Create Node without Property

    CREATE (E: employee)
    create (D: Department)


Create Node with Property

    CREATE (B: Books {
        bid: 1,
        bname: 'Book 1',
        aid: 1
    })

    CREATE (B2: Books {
        bid: 2,
        bname: 'Book 2',
        aid: 1
    })

Another way to Create Node with Property

    CREATE (B: Books) 
	SET		B.bid = 3,
		    B.bname = 'Book 3',
        	B.aid = 2

Create Multiple Node

    CREATE (A: Authors {
        aid: 1,
        aname: 'Author 1'
    }), (A2: Authors {
        aid: 2,
        aname: 'Author 2'
    })

Another way to Create Node with Property

	CREATE (B: Books), (B2: Books) 
	SET		B.bid = 3,
			B.bname = 'Book 3',
        	B.aid = 2
	SET		B2.bid = 3,
			B2.bname = 'Book 3',
        	B2.aid = 2	

>- 'E' is the node name and it is just an alias in this cmd only, It will not store in db.
>- employee in the label name which can be more then one and more then one label can contains more then one node.
>- Label is like the name of table but in graph database we didn't name have tables it is just for understanding.
>- Will user this cmd to insert (create) record (node) in db which can be represent via label.
>- if we didn't enter properties then will be create node with empty properties.
>- command are not case sensitive.
>- Always give label otherwise when retrieving data we will not able to only target that data because will be given all data.
>- To create multiple node in single cmd, we have to separate nodes in comma and change the node name.

####Neo4j CQL MATCH & RETURN

MATCH is like select cmd in SQL for define which node/ label and what property where RETURN will gives us back the data.

    MATCH (b: books)
    RETURN B

>This give us error because node and label name is case sensitive and it is not necessary to give same node name which was given when create because node is only represent data in active cmd

    MATCH (B: Books)
    RETURN B
    MATCH (A: Authors)
    RETURN A
    MATCH (B: Books), (A: Authors)
    RETURN B, A
    
>Always mentioned label name otherwise it will pull all data

    MATCH (B: Books)

>Will get all books from database

    MATCH (B: Books {aid: 1})

>Will get books having aid = 1 from database, it is also working like WHERE cmd but we also have WHERE cmd who set filter on data which is get MATCH cmd not database 

     MATCH (B: Books), (A: Authors) RETURN B,A

>This will return two json object

    MATCH (B: Books), (A: Authors) RETURN B.bid, B.bname, A.aname

>This will return one son object contain fields which we have specified, Note: at this point we get data multiplied because no relationship is created.

####Neo4j CQL RELATIONSHIP

Relationship is not like join in sql because we have structure free database so there are no tables in which we can create join.

Therefore what will be in relationship, actually relationship represent the connection between two nodes and can have connection properties. Like…

######Relationship will be create for each node not for a single standard like joins and it can be multiple

    MATCH (A: Authors { aid: 1}), (B: Books { aid: 1}) 
    CREATE (A) - [R: AUTHOR_OF] -> (B)

Another way to create relationship

    MATCH (A: Authors ), (B: Books)
    WHERE A.aid =1 AND  B.aid = 1
    CREATE (A) - [R: AUTHOR_OF] -> (B)

>This will create relationship between all nodes of authors having aid = 1 and all nodes of books having aid = 1

######Carefull

    MATCH (A: Authors ), (B: Books)
    WHERE A.aid =  B.aid
    CREATE (A) - [R: AUTHOR_OF] -> (B)

>This will create relationship between all node of authors and all nodes of books where both have same aid.
>Make sure before using this query because it will also create relationship for which relationships already made in same criteria like previous example.
>This would be help full when you import data and want to create relationship between all nodes. 

######Important

>It is important to describe the relation name correctly because it will let you remind that what direction is set and what was the position of node at the time of creation as when we will query the relationship it will return data what we give direction in this query and node will be set as per direction. 


######Relationship with Property

    MATCH (A: Authors ), (B: Books)
    WHERE A.aid =1 AND  B.bid = 1
    CREATE (A) - [R: AUTHOR_OF] -> (B)
    SET R.createdDate = "15/10/2012",
		R.publishedby = "ENY Publisher", 
		R.edition = "1st"

>- This will create relationship with all nodes of authors having aid = 1 with the all nodes of books have bid = 1 with the properties.
>- In the previous example all books were connect to author where in this example we are connecting only one book because each book have it connection property like each book were created on separate date and published by separate publisher and have multiple edition.
