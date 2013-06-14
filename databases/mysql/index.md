##MySQL Databases

###Configure

Before you can connect to a database you will need to configure your database.
This is done by adding the database details to your configuration (ini) file
under the [database] and [database\db] sections.

To add the basic configuration of a MySQL database to your project,
add the following to “config/defaults.ini” then modify the hostname,
username, password and database to suit your setup:

  [database]
  factory = \Cubex\Database\DatabaseFactory
  engine  = mysql

  [database\db]
  register_service_as = db
  hostname = localhost.dev
  username = root
  password =
  database = cubex

###Multiple Databases

The above example would be fine for a single database project, if you require
access to multiple MySQL databases, you might use something like the following:

  [database]
  factory = \Cubex\Database\DatabaseFactory
  engine  = mysql

  [database\accountsdb]
  register_service_as = accountsdb
  hostname = localhost.dev
  username = accounts_user
  password =
  database = accounts

  [database\ordersdb]
  register_service_as = ordersdb
  hostname = localhost.dev
  username = orders_user
  password =
  database = accounts

The “register_service_as” will later allow us to access the database object
via the Cubex “Service Manager” (using the specified value).
