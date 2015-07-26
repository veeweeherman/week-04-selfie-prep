# Databases
a change for changes sake

<!--MARCUS NEEDS TO BUILD THIS COMMENT OUT MORE: This is a sprint where you will be required to be a scribe. Specifically, you'll at least be expected to understand which queries will be slow, and why. ...something
about joins and join tables?-->

---

## Installation and Getting Started

### Installation

Ensure you have mysql installed by doing `which mysql`. If you don't have it,
install mysql using `brew install mysql`.

### Getting Started

- Start up mysql using `mysql.server start`
- Start up your mysql server by logging in using `mysql -u root`
- Load your schema using `mysql -u root < server/schema.sql` on
  the command line

**NOTE**: Using `mysql -u root` sets up your username to be `root`,
you will need to fill this information into the tests to get them
to run.
  
##### Start a local MySql server

Now that the tutorials have given you an overview of SQL, try it out on a real
database! MySQL server is already installed on your machine. But just as you
must start the Node.js servers you've written with a command like `node
server.js`, you must start the MySql server before it will be of any use to
you.

- [ ] Stop any MySql servers that are already running (they may have been spun up automatically when you're computer was booted) by running `mysql.server stop`
- [ ] Start a local MySql server by running `mysql.server start`

##### Create a MySql database

- [ ] Log into MySQL on the command line with `mysql -u root`.
- [ ] Learn about how to [Create a database from the command line], then choose one of your schema designs from the tutorial step and create the table using the CREATE TABLE statement.
- [ ] INSERT some made-up data into it and SELECT the data back out.
- [ ] Log into MySQL from the command line again and use `DESCRIBE TABLE` to verify that it was created correctly.

### Part Two - Advanced Data Storage

## REPO Structure

#### server:

* `schema.sql` is a skeleton schema file. In this file you should write one or
  more `CREATE TABLE` statements that will define the structure of your
  database tables. You can then create the tables for real by running the
  schema file on the command line.
  * **NOTE**: if you run your SQL code from this file, and find a bug in the schema
    or how it was generated, you'll want to "drop" all the new tables before
    running it again. This will reset your database by throwing away all data
    and schema information, to give you a blank slate before re-running your
    improved version of the SQL code.
  * You don't have to manually write your schema, you may use a visual schema
    designer.[WWW SQL Designer] or [DB designer] are good places to start.
* `app.js` will be the main file of your Node server code, just
  like `basic-server.js` in the previous assignment. It includes some code
  showing how to use Node's `mysql` module to connect to the database.
* `spec` contains a mocha spec for testing your Node server's ability to read
  and write the database. This spec is not complete! It contains several lines
  commented with "TODO". You'll need to customize those lines to match the
  details of the database tables you create.

#### client

* An empty folder for you to put your client in. Either use your
  chatterbox-client implementation, or, if there is something irreparably wrong
  with your solution, use the Hack-Reactor-provided solution.

#### orm-resources:

* `orm-example.js` contains **EXAMPLE CODE** for you to reference when
  refactoring your server to use the Sequelize ORM from Node to read and write
  data to the MySQL database instead of raw SQL strings.
* When you get to the ORM refactoring stage, copy your old server code to a
  `server-pure-sql` folder, then make your refactors in-place in the `server`
  folder. This way you will have both versions in your liberated repo, so
  everyone can see that you are awesome with both technologies!

---

## Basic requirements

### Section 1:

- [ ] Design a normalized (multi-table) schema to hold data for your chatterbox-server. Edit the file `server/schema.sql` to define the table (or tables) you want, then create the database with your schema using `mysql -u root < path/to/schema.sql`. Log into MySQL from the command line again and use `DESCRIBE TABLE` to verify that it was created correctly.
- [ ] Use npm to install (and save) the `mysql` module using `npm install mysql --save` so your chatterbox-server is able to talk to MySQL.
- [ ] Take a look at the tests in `server/spec/server-spec.js`. Before you start hacking on your persistent server, read the tests and try to understand what they're trying to do.
  - [ ] **NOTE**: The tests depend on the details of the schema you created,   so you will need to customize the spec file with some of these details before it will be able to run.
- [ ] Put all the pieces together to create a persistent SQL-backed chatterbox-server! Use `server/app.js` as your main file. You can copy over js files from your chatterbox-server assignment and `require` them into `server`.
  * Note: This will mean you remove the in-memory messages array that used to store your data as part of the node process. Every new message will result in a write to the database, and every request for data will result in a read. You should no longer need to cache any of that data in memory as part of the application.
- [ ] Have your server connect to MySQL, and use the database connection to store data as messages come in.
- [ ] Manually test your server's persistence: Send some chat messages to your server, then stop Node. Start your server up again, connect to it with the client, and see whether the messages you sent last time are still there! Finally, make all the unit tests pass and write some more of your own!

### Section 2:

- [ ] Install Sequelize using `npm install --save sequelize`.
- [ ] Read the Sequelize docs and the example code in `orm-resources/orm-example.js` to understand how the ORM works.
- [ ] Refactor your existing server to use Sequelize.
 Since you haven't modified your server's HTTP interface or the database schema (right?), the old unit tests should still work without modification.
  * Note that this is one of the biggest wins from consistent testing: They let you refactor and rewrite your code with confidence, since they'll tell you if you broke anything that used to work.



## Docs

### Relevant ORM documentation

* [Sequelize ORM for Node]
* [Object Relational Mapping - Wikipedia]

[Relational Databases]:https://en.wikipedia.org/wiki/Relational_database
[WWW SQL Designer]:http://ondras.zarovi.cz/sql/demo/
[DB designer]:http://dbdsgnr.appspot.com/
[SQLCourse.com]:http://www.sqlcourse.com/intro.html
[WWW SQL Designer]:http://ondras.zarovi.cz/sql/demo/
[Create a database from the command line]:http://www.linux.org/article/view/create-mysql-database-via-command-line
[MongoDB tutorial]:http://docs.mongodb.org/manual/tutorial/getting-started/
[map-reduce query]:http://docs.mongodb.org/manual/applications/map-reduce/
[Memcached]:http://www.memcached.org/
[Introduction to SQL tutorial]:http://www.sqlcourse.com/intro.html
[Interactive tutorial on SQL]:http://sql-pql.herokuapp.com/
[MySQL CREATE TABLE reference docs]:https://dev.mysql.com/doc/refman/5.1/en/create-table.html
[MySQL SELECT reference docs]:https://dev.mysql.com/doc/refman/5.0/en/select.html
[MySQL INSERT reference docs]:http://dev.mysql.com/doc/refman/5.5/en/insert.html
[Node mysql module docs]:https://github.com/felixge/node-mysql
[Executing SQL statements from a file]:https://dev.mysql.com/doc/refman/5.0/en/batch-commands.html
[Sequelize ORM for Node]:http://sequelizejs.com/
[Object Relational Mapping - Wikipedia]:http://en.wikipedia.org/wiki/Object-relational_mapping
[Starting and stopping MongoDB]:http://www.mongodb.org/display/DOCS/Starting+and+Stopping+Mongo
[Using MongoDB from the command line]:http://docs.mongodb.org/manual/tutorial/getting-started/
[MongoDB module for Node]:https://github.com/christkv/node-mongodb-native#readme
[Memcached site]:http://www.memcached.org/
[Node-memcached module]:https://github.com/3rd-Eden/node-memcached
[A Visual Explanation of SQL Joins]:http://www.codinghorror.com/blog/2007/10/a-visual-explanation-of-sql-joins.html
[SQLfiddle]:http://sqlfiddle.com/
[MySQL Workbench - robust MySQL design tool]:http://dev.mysql.com/downloads/workbench/

