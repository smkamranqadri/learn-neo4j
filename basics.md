### Basics

>Neo4j Graph Database has mainly the following building blocks...

>- Nodes
>- Properties
>- Relationships
>- Labels

####Node

>Node is a fundamental unit of a Graph. It contains properties with key-value pairs as show below

    { 
        firstNmae : "Muhammad"
        lastNmae : "Kamran"
    }
    
####Properties

>Above code represnt the Node in which you can find two **Properties** Where **"firstName"** is Key and **"Muhammad"** is Value

####Relationship

>Relationship are another major building block of a Graph Database, it connects two nodes as show below.

    Emp - WORKS_FOR -> Dept

>Here Emp and Dept are two different node. WORKS_FOR is relationship between Emp and Dept nodes.

>As Neo4j is schema free so it means that no table, no column, no row then no join so what does relationship do, Actually it is also a record which create the join and you can also save properties in it.

>So relationship will be between each record (node) so we need to create relatioship whenever create record (node).  

####Labels

>Labels are like the table name but we can associate one label with multiple record (node) or relationship.
