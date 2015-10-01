---
title: "Troubleshooting Apps"
---
## Problem: I don't know if my app is compatible with Convox.

**Solution: Run `convox init && convox start` in your application directory.**

`convox init` automates creating the right `Dockerfile` and `docker-compose.yml` manifest if those files are not already present.

`convox start` is a tool that builds and runs your application in your local development environment using Docker.

The experience of a single `convox start` command to start a development environment is something all developers will enjoy.

## Problem: I get an error when I deploy my app to Convox

**Solution: Run `convox logs --app convox` to inspect the Convox API logs for errors and `convox deploy` to deploy again**

In one terminal window, run `convox logs --app convox` to get a feed of your deployment API logs. In another terminal run `convox deploy`. If your deploy always errors, either [open an issue on GitHub](https://github.com/convox/kernel/issues) or send support@convox.com a report. Include the deploy output and the deployment API logs.

## Problem: My app deployed but I can not access it

**Solution: Run `convox logs` to inspect your application logs and cluster events for problems placing your container, starting your app, and registering with a load balancer**

Sometimes subtle configuration problems prevent your app from booting successfully.

Run `convox logs` to access your application logs for errors. A common problem is the app failing to start due to missing environment variables. Set all environment variables you need with `convox env` to boot your app.

## Problem: Convox deploy hangs at 'Waiting for app...'

**Solution: Ensure that your application is bound to 0.0.0.0, not 127.0.0.1. Otherwise diagnose with `convox logs` as described above.
