---
title: "@OneToMany relationship with JPA and Hibernate"
written by: Rohit Singh Bhandari
date: 2023-04-22T15:07:22+05:30
draft: false
---

# Introduction

In a relational database system, a one-to-many association links two tables based on a Foreign Key column so that the child table record references the Primary Key of the parent table row.

**Mapping**

We have two choices for that:
1. a unidirectional @OneToMany association
2. bidirectional @OneToMany association

    The bidirectional association requires the child entity mapping to provide a @ManyToOne annotation, which is responsible for controlling the association.
    On the other hand, the unidirectional @OneToMany association is just the parent-side that defines the relationship.

# Unidirectional @OneToMany

```
@Entity
@Data
@Table(name = "orm_user")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Integer userId;
    private String userName;

    @OneToMany(cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Address> addresses = new ArrayList<>();
}
```java


```
@Data
@Entity
@Table(name = "orm_address")
public class Address {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Integer addressId;
    private String street;
    private Integer zipCode;
    private String city;
    private String country;
}
```java


**@GeneratedValue**: If we want to automatically generate the primary key value, we can add the                         @GeneratedValue         annotation. This can use four generation types: AUTO, IDENTITY, SEQUENCE and TABLE. If we don't explicitly specify a value, the generation type defaults to AUTO

**cascade**: Entity relationships often depend on the existence of another entity, for example shown here user–Address relationship. Without the user, the Address entity doesn't have any meaning of its own. When we delete the user entity, our Address entity should also get deleted.
        **Cascading is the way to achieve this. When we perform some action on the target entity, the same action will be applied to the associated entity.**

**orphanRemoval**: Its usage is to delete orphaned entities from the database. An entity that is no longer attached to its parent is the definition of being an orphan.

    Since we are not using mappedBy and @JoinColumn, hibernate will make three table for that.
1. user table
2. address table
3. user_address_table (table for mapping)

Let's assume we are inserting data of a user and it's three different addresses(Assumed-data).
subsequently when we hit APIs and insert data, it executes following SQL queries:

```
insert into user (userId, userName)
values (1,"Rohit")
 
insert into address (addressId,street,zipCode,city,country)
values (2,Add1,1235,Add1,Add1)
 
insert into address (addressId,street,zipCode,city,country)
values (3,Add2,1245,Add2,Add2)
 
insert into address (addressId,street,zipCode,city,country)
values (4,Add3,1345,Add3,Add3)
 
insert into user_address_table (userId, address_id)
values (1, 2)
 
insert into user_address_table (userId, address_id)
values (1, 3)
 
insert into user_address_table (userId, address_id)
values (1, 4) 
```java

*What is that! Why there are so many queries executed? And what’s the deal with that user_address_table table anyway?*
        Well, by default, that’s how the unidirectional @OneToMany association works.
Instead of two tables, we have three tables here, so we are using more storage than necessary. Instead of only one Foreign Key, we now have two of them(Entire third table). However, since we are most likely going to index these Foreign Keys, we are going to require twice as much memory to cache the index for this association. 
Quite in-efficient right...?

# Unidirectional @OneToMany with @JoinColumn

To fix that extra join table issue, we need to add @JoinColumn.
The @JoinColumn annotation helps us specify the column we'll use for joining an entity association or element collection.
        In a One-to-Many/Many-to-One relationship, the owning side is usually defined on the many side of the 
relationship. It's usually the side that owns the foreign key. The @JoinColumn annotation defines that actual physical mapping on the **owning side**.
Here address entity is joining side so we'll use @JoinCoulmn annotation there:

```
...
@OneToMany(cascade = CascadeType.ALL, orphanRemoval = true)
@JoinColumn(name = "user_id")
private List<Address> addresses = new ArrayList<>();
...
```java

The @JoinColumn annotation helps Hibernate to figure out that there is a user_id Foreign Key column in the address table that defines this association.

*With this annotation in place, when persisting the three PostComment entities, we get the following SQL output:*

```
insert into user (userId, userName)
values (1,"Rohit")
 
insert into address (addressId,street,zipCode,city,country)
values (2,Add1,1235,Add1,Add1)
 
insert into address (addressId,street,zipCode,city,country)
values (3,Add2,1245,Add2,Add2)
 
insert into address (addressId,street,zipCode,city,country)
values (4,Add3,1345,Add3,Add3)

update address set user_id = 1 where id = 2

update address set user_id = 1 where id = 3

update address set user_id = 1 where id = 4
```java

        Well, a bit better! atleast we got rid three tables to two tables now.
but what’s the purpose of those three update statements?
Here foriegn key updation statements got executed after the data got inserted to DB. Hibernate inserts the child records first without the Foreign Key since the child entity does not store this information. During the collection handling phase, the Foreign Key column is updated accordingly.


# Bidirectional @OneToMany

The best way to map a @OneToMany association is to rely on the @ManyToOne side to propagate all entity state changes:

```
@Data
@Entity
@Table(name = "orm_user")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Integer userId;
    private String userName;


    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Address> addresses = new ArrayList<>();
}
```java

```
@Data
@Entity
@Table(name = "orm_address")
public class Address {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Integer addressId;
    private String street;
    private Integer zipCode;
    private String city;
    private String country;

    @ManyToOne
    private User user;
}
```java

Again we run our application, hit APIs and insert the same pre-assumed data. 
Hibernate generates just one SQL statement for each persisted PostComment entity:

```
insert into user (userId, userName)
values (1,"Rohit")
 
insert into address (addressId,street,zipCode,city,country)
values (2,Add1,1235,Add1,Add1)
 
insert into address (addressId,street,zipCode,city,country)
values (3,Add2,1245,Add2,Add2)
 
insert into address (addressId,street,zipCode,city,country)
values (4,Add3,1345,Add3,Add3)
```java

   Finally, the number of queries are reduced.
Think of an application in macro level where in each second millions of requests are hitting the server, in the above shown unidirectional mapping it will generate a lot more queries as compared to bidirectional mapping.
If the application would be in bidirectional mapping then certainly it will have more space to breathe as compare to otherwise.   
    **So, the bidirectional @OneToMany association is the best way to map a one-to-many database relationship when we really need the collection on the parent side of the association.**

# Conclusion

Bidirectional @OneToMany associations are way better than unidirectional ones because they rely on the @ManyToOne relationship, which is always efficient in terms of generated SQL statements.
       But then, even if they are very convenient, you don’t always have to use collections. The @ManyToOne
association is the most natural and also efficient way of mapping a one-to-many database relationship.   
   


