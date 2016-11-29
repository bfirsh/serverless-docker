# Serverless Docker

Swarm makes it incredibly easy to run code on your infrastructure. You wrap some code up inside a Docker container, and Swarm will make it run on whatever free resources you have.

But what if those containers could also run other containers on a Swarm? We could put pieces of our application inside containers that are run on-demand on a Swarm. Docker containers can be used as functions from within other applications:

```python
>>> import dockerrun
>>> client = dockerrun.from_env()
>>> client.run("bfirsh/leftpad", ["foo", "5"])
'  foo\n'
```

Take, for example, running background tasks in a web app. In a traditional architecture, you would have a set of task workers and a message queue to pass work from the web frontends to the task workers.

If your web frontends have access to a Swarm, you can run the task directly on your Swarm:

```python
client.run("tasks/reticulate-splines", detach=True)
```

To read more about this, [check out this blog post](https://blog.docker.com/2016/06/building-serverless-apps-with-docker).

## Examples

 - [Serverless voting app](https://github.com/bfirsh/serverless-docker-voting-app) – A serverless web app
 - [go-dexec examples](https://github.com/ahmetalpbalkan/go-dexec/tree/master/examples)
 - [Funker](https://github.com/bfirsh/funker-example-voting-app) – an example app that uses Funker to do processing in the background

## Reading

 - [Introducing dexec](https://ahmetalpbalkan.com/blog/dexec/) – What if the Go os/exec library could containerize?

## Tools

 - [Funker](https://github.com/bfirsh/funker) – Functions as Docker containers
 - [go-dcgi](https://github.com/bfirsh/go-dcgi) – CGI, but with Docker containers

## Client libraries

 - [docker-py](https://github.com/docker/docker-py) – Run Docker containers from Python apps
 - [dockerrun](https://github.com/bfirsh/dockerrun) – A simpler interface for running Docker containers in Python (soon to be part of docker-py)
 - [go-dexec](https://github.com/ahmetalpbalkan/go-dexec) – Like Go os/exec package but for Docker
 - [dockerode](https://github.com/apocas/dockerode) – Run Docker containers from Node.js apps
 - [docker-java](https://github.com/docker-java/docker-java) – Run Docker containers from Java apps

## Stuff that needs working on

We need your help!

 - Make this work with Docker 1.12.
 - A proxy that scopes a Docker API so that containers can securely manage and run "child" containers.
 - Helpers for injecting the Docker API socket into containers that are run.
 - A server for running scheduled / cron jobs as Docker containers on a Swarm.
