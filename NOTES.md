# Brief Notes on System Design
## Extra Links
[Scaling Dropbox](https://www.youtube.com/watch?v=PE4gwstWhmc&t=1s)

[Distributed Systems](https://www.youtube.com/watch?v=Y6Ev8GIlbxc&t=0s)

[The Paper Trail (Distributed Systems Blog)](https://www.the-paper-trail.org/)
## VPS vs Webhosted
VPS (virtual private server)
- you get a sectioned off VM rather than sharing resources with other people

## Databases
#### Scalability Approaches
1. Master-slave replication - this will likely requiring lots of expensive scaling up
2. Denormalization - denormalizing data will mean that we have fast query times that may be better suited for NoSQL databases which become much more scalable as we add to the DB cluster
### Normalization
> Normalizing means to 
### Denormalization
> Denormalizating means to first normalize our data and then optimize data retrieval by delibrately keeping redundant data to increase performance by reducing the need for costly joins on tables, or to store pre-calculated values to remove the need to calculate them at the time of query execution.
In this manner we can have pre-joined tables to remove the need for a join at query time.
#### Advantages
1. Optimize Query Performance - redundant data requires less need for joins thereby increasing the speed at which queries return.
2. Ease of Management - redundant data means less tables to manage, and less to worry about for calculations done at execution time.
#### Disadvantages
1. Costly Updates - redundant data means that we need to make lots of WRITE operations in order to change one value
2. Potential Inaccuracies - data that is repeated has the greater potential for either being entered wrong
## Caching
> A cache holds the most recently accessed queries done on a database (in redis and memcached cases, they hold it in memory!) and acts as a faster alternative between the requestor and the datastore.
### Caching Patterns
1. Query Caching - store resulting datasets of a query in memory (i.e. SELECT * FROM table). Although expiration becomes a problem when updates are done to table.
2. Object Caching - 

# Notes From CS75 Lecture
## VPS vs Webhosted
VPS (virtual private server)
- you get a sectioned off VM rather than sharing resources with other people
## Scaling
### Vertical Scaling
Or scaling up, is a solution in which you add more resources to the machines in use. Limited by how much resources you can add to the systems
### Horizontal Scaling
Architecting the system to buy a greater number of cheaper servers rather than improving existing (expensive) server resources
Creates the problem of how to balance request loads
#### Load Balancing
What IP to show the requestors of a website? Show the load balancers IP and let all requests be handled by the load balancer.
How to balance the load?
- high load vs low load
- dedicated servers (one handles the html code, one handles the jpgs one handles the gifs and route accordingly)
- round robin (this breaks when we have one requestor -sent to server N- requesting multiple times, we don't want them to be going to different servers to restart cached sessions from server N-1 )
    - we can have a shared session server that saves sessions to prevent this, but what if that server goes down?

## RAID
RAID0 (striping)
- splitting data writes to each disk 
- nice for performance

RAID1 (data mirroring)
- writing in parallel
- data redundancy

RAID10 (striping and redundancy)
- both RAID0 and RAID1

RAID5 (3+ drives, 1 used for redundancy)

RAID6 (3+ drives, 2 used for redundancy)
## Database Replication
For read heavy applications, it is often useful to have a master-slave relationship in which the slave is able to handle read requests while write requests go through the master.
