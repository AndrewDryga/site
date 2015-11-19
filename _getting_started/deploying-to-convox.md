---
title: "Deploying to Convox"
sort: 30
---
Applications can be deployed to Convox via the `convox deploy` [CLI](https://github.com/convox/cli) command. To quickly see Convox deployment in action, you can clone our Sinatra [example app](https://github.com/convox-examples/sinatra).

    $ git clone https://github.com/convox-examples/sinatra.git

### Create the app

Change into the sinatra directory and create the application.

    $ cd sinatra
    $ convox apps create sinatra

### Create the backing services

When you create a new app, Convox provisions all of the AWS infrastructure required to support your core application. You'll also need to create the Postgres and Redis services that this app needs:

    $ convox services create postgres pg1
    Creating pg1 (postgres)... CREATING

    $ convox services create redis rd1
    Creating rd1 (redis)... CREATING

<div class="block-callout block-show-callout type-info">
  <p>Each of these services will take a few minutes to create. You can see the current status with `convox services`.</p>
</div>

### Set the environment

Once the service creation is complete, set the `POSTGRES_URL` and `REDIS_URL` environment variables. You can fetch these URLs using the `convox services info` command. Note that your passwords will be different than those shown here.

    $ convox services info pg1
    Name    pg1
    Status  running
    URL     postgres://postgres:KEDS6tKPZb1iffVB8IXi@pg1.cbm068zjzjcr.us-east-1.rds.amazonaws.com:5432/app

    $ convox env set POSTGRES_URL=postgres://postgres:KEDS6tKPZb1iffVB8IXi@pg1.cbm068zjzjcr.us-east-1.rds.amazonaws.com:5432/app

    $ convox services info rd1
    Name    rd1
    Status  running
    URL     redis://u:Rn2uRT7g7NJ8iXNAtnSj@rd1-Balancer-124JJ4R695MAR-153811640.us-east-1.elb.amazonaws.com:6379/0

    $ convox env set REDIS_URL=redis://u:Rn2uRT7g7NJ8iXNAtnSj@rd1-Balancer-124JJ4R695MAR-153811640.us-east-1.elb.amazonaws.com:6379/0

### Deploy the app

Use the `convox deploy` command to deploy the app. The Convox CLI will print live updates as the deployment proceeds.

    $ convox deploy
    Uploading... OK
    RUNNING: docker build -t xmjsczmcug /tmp/repo044075326/clone
    Sending build context to Docker daemon 92.16 kB
    Sending build context to Docker daemon
    Step 0 : FROM ruby:2.2.2
    2.2.2: Pulling from ruby
    ...

When the build finishes the release ID will be shown.

    Releasing... OK, RANLOWQFMRF

The CLI will wait for the app's load balancer to become available.

    Waiting for app...

When the load balancer becomes available the deploy is finished. Any processes with open ports will be listed.

    web: http://sinatra-1233165548.us-east-1.elb.amazonaws.com:3000 
