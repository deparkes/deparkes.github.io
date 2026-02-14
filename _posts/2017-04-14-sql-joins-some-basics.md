---
layout: post
title: 'SQL Joins: Some Basics'
date: 2017-04-14 15:30:20.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- data
tags:
- data
- database
- joins
- matching
- sql
- sql joins
author: deparkes
permalink: "/2017/04/14/sql-joins-some-basics/"
---
Joining tables in <a href="https://en.wikipedia.org/wiki/SQL">SQL </a>is an <a href="https://www.linkedin.com/pulse/why-you-should-learn-sql-brewster-knowlton">essential </a>part of many digital services and products. Joins let you answer questions such as which customers bought which products? How many staff work at a particular location? Which students are in which classes at a school? Joining in SQL becomes even more important when your data are stored in a <a href="https://en.wikipedia.org/wiki/Database_normalization">normal form</a>.
Different types of join are possible in SQL, and each has different uses and strengths. There are already some excellent resources available online that talk through different aspects of SQL joins such as <a href="https://www.youtube.com/watch?v=SmDZaH855qE">Youtube</a>, or <a href="https://stackoverflow.com/questions/38549/what-is-the-difference-between-inner-join-and-outer-join">Stack Overflow</a>.  This post is a quick general overview of the keys points about SQL joins.
<h1><strong>What is a join?</strong></h1>
Joining in SQL is all about linking database tables in a meaningful way. But before we think about databases, let's think about what we might do in the "real world".
As an example let's think about a teacher who keeps some lists about clubs at his school. He has a list of the club names, and details about the club activities. He would like to know which pupils  are involved in each  club. He speaks to the pupils to ask them each which clubs they are involved in. He now has two lists, or tables:
one with information about clubs,

| ![sql joins - clubs table]({{site.url}}/assets/2017/04/clubs.png) |
|:--:|
| *sql joins - clubs table* |

and one with information about pupils:

| ![sql joins - pupils table]({{site.url}}/assets/2017/04/pupils.png) |
|:--:|
| *sql joins - pupils table* |

Since our teacher wants to know about a combination of pupils and clubs, he will need to somehow join his two lists. To do his ''join" he can print out a copy of the two lists. He can go down each row in his list of clubs, and then looks through his list of pupils to see which pupils are involved, and make a note in a new table.
<h1>It Depends What We Want to Know</h1>
At this stage the teacher has a choice he can make about the information he cares about.  For example, does he want to know:
<ol>
<li>All combinations of pupils and clubs?</li>
<li>Information about all clubs, even if they don't have any pupils in them?</li>
<li>Information about all pupils, even if they aren't involved in any clubs?</li>
<li>Only about clubs where there are corresponding pupils?</li>
<li>Or all information about both clubs and pupils, even if they have no pupils or are involved in no clubs?</li>
</ol>
Right away some of these seem more useful than others, but they do each correspond to a type of 'join' he could do. Which join he selects will depend on exactly what he is interested in.
Maybe he is concerned that some pupils are not involved in any clubs and might be missing out - in which case he would want to include all pupils.
It might be that the school has a policy of giving cupboard space to all clubs, but if there aren't any pupils in the club, this space could be freed up - in which case he would want to include all clubs, but would not be so concerned about pupils not in clubs.
It's also possible that he would like to know about active clubs and their associated pupils, in which case he would only want a list which ignored empty clubs or inactive pupils.
These scenarios faced by our example teacher are just like the SQL joins available too us. Let's looks again at this teacher example using SQL language.
You can have a play around with the SQL used in these examples <a href="https://rextester.com/WGJXL98567">here</a>.
<h1>Types of SQL Join</h1>
<h2><strong>Cross Join - All Combinations of pupils and clubs</strong></h2>
The cross join is also known as a <a href="https://www.tutorialspoint.com/sql/sql-cartesian-joins.htm">Cartesian join</a>, and is on the face of it <a href="https://stackoverflow.com/questions/2380194/where-are-cartesian-joins-used-in-real-life">not all that useful</a> - there aren't too many situations where knowing all possible combinations is useful on itself. It is still good to know about it though. The cross join is all possible combinations of the two table so it can be helpful to think of other joins as almost like filters or modifiers of the rows in the cross join.
In SQL we would have:

```sql
SELECT *
FROM   pupils
       CROSS JOIN clubs;
```

which gives the cross join output:

| ![sql joins - cross join]({{site.url}}/assets/2017/04/cross_join.png) |
|:--:|
| *sql joins - cross join* |

I have highlighted here the rows that correspond to the inner join, below.
<h3><a href="https://www.sqlguides.com/sql_cross_join.php">Read more about cross joins</a></h3>
<h2><strong>Inner join - just the active clubs and pupils</strong></h2>
The inner join is often the '<a href="https://stackoverflow.com/questions/565620/difference-between-join-and-inner-join">default</a>' type of join that people think of - it returns rows where there is a match on the fields you are joining on. This is what the teacher would use to get a list of the active clubs and associated pupils - he could join on the 'club name' field.
In SQL we can write

```sql
SELECT pupils.NAME,
clubs.club_name
FROM pupils
INNER JOIN clubs
ON pupils.club = clubs.club_name;
```

which gives:

| ![sql joins - inner join]({{site.url}}/assets/2017/04/inner_join.png) |
|:--:|
| *sql joins - inner join* |

An inner join won't give you any information about the items in each list which didn't match. The rows that didn't have a match are missed out.
In terms of the cross join mentioned above, we can imagine the cross join (all combinations of rows from both tables), and keep only the rows where there is a match on the fields we are joining on.
<h3><a href="https://www.w3schools.com/sql/sql_join_inner.asp">Read more about inner joins</a></h3>
<h2><strong>Outer joins</strong></h2>
Outer joins preserve the non matching rows from both the left and the right tables. The inner join discards any rows which don't match. Outer joins let us keep these, even if a match between the two ta Les isn't found. I talk below about left and right outer joins - really left and right just depend on how we think of our tables.
<h2><strong>Left Outer Join - we also want to know about pupils without a club
</strong></h2>
These are also sometimes just called left joins. One of the options our example teacher might care about is to see which pupils have not been getting involved in club activities. To include these rows we need to use a left outer join. ( Whether we use left or right outer join just depends on which table we consider to be "left" and which one "right").
In SQL we would write:

```sql
SELECT pupils.NAME,
clubs.club_name
FROM pupils
LEFT OUTER JOIN clubs
ON pupils.club = clubs.club_name;
```


Which returns:

| ![sql joins - left outer join]({{site.url}}/assets/2017/04/left_outer_join.png) |
|:--:|
| *sql joins - left outer join* |

<h3><a href="https://www.dofactory.com/sql/left-outer-join">Read more about left outer joins</a></h3>
<h2><strong>Right Outer Join - we also want to know about clubs without any pupils
</strong></h2>
Sometimes​ just called right joins, these joins are conceptually the same as left joins. The only difference comes in how we think of the two tables we are joining. The right join allows us to capture the null rows of our right hand table - in this case the clubs without any pupils as members.

```sql
SELECT pupils.NAME,
       clubs.club_name
FROM   pupils
       RIGHT OUTER JOIN clubs
                     ON pupils.club = clubs.club_name;
```

Which returns:

| ![sql joins - right outer join]({{site.url}}/assets/2017/04/right_outer_join.png) |
|:--:|
| *sql joins - right outer join* |

<h3><a href="https://www.w3schools.com/sql/sql_join_right.asp">Read more about right outer joins</a></h3>
<h2><strong>Full Outer join - we want to see both pupils and clubs whether the are connected or not.</strong></h2>
The full outer join brings with it the rows which didn't have a corresponding entry in the other table. The full outer join is less commonly used than the other joins, but <a href="https://stackoverflow.com/questions/2094793/when-is-a-good-situation-to-use-a-full-outer-join">does have its uses</a>. In our example we can use it to see both pupils without a club, and clubs without pupils.

```sql
SELECT pupils.NAME,
clubs.club_name
FROM pupils
FULL OUTER JOIN clubs
ON pupils.club = clubs.club_name;
```

Which returns:

| ![sql joins - full outer join]({{site.url}}/assets/2017/04/full_outer_join.png) |
|:--:|
| *sql joins - full outer join* |
