---
title: "PostgreSQL"
---
### Creating a database

You can create PostgreSQL databases using the `convox services create` command. For example, to create a database called "pg1", use the following command:

    $ convox services create postgres --name pg1
    Creating pg1 (postgres)... CREATING

This kicks off the provisioning of a Postgres database on the Amazon RDS service. Creation can take up to 15 minutes. To check the status of the DB creation, use the command specified in "Database Info" below. The status will be 'creating' until the database becomes available.

### Database info

To see relevant info about the database, use the `convox services info` command.

    $ convox services info pg1
    Name    pg1
    Status  running
    URL     postgres://postgres::)t[THpZ[wmCn88n,N(:@pg1.cbm068zjzjcr.us-east-1.rds.amazonaws.com:5432/app

Add the URL to the environment of any app that needs to use the database. Make sure to put quotes around the string to avoid issues with invalid characters:

    $ convox env set 'DATABASE_URL=postgres://postgres::)t[THpZ[wmCn88n,N(:@pg1.cbm068zjzjcr.us-east-1.rds.amazonaws.com:5432/app' --app myapp

### Deleting a database

To delete the database, use the `convox services delete` command:

    $ convox services delete pg1
    Deleting pg1... DELETING

Deleting can take several minutes. Use `info` to check on the status if you like. The info command will return a status of 'deleting' until the service is successfully deleted.

### Using a third-party database

You can use other hosted database services with your Convox app. Just set the environment varaible(s) that your app needs to connect as shown above.
