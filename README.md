# Serverless Docker

A simpler, more scalable way of writing distributed apps.

Swarm makes it incredibly easy to run code on your infrastructure. You wrap some code up inside a Docker container, and Swarm will make it run on whatever free resources you have.

But what if those containers could also run other containers on a Swarm? We could put pieces of our application inside containers that are run on-demand on a Swarm. Docker containers can be used as functions from within other applications:

```bash
$ docker run myapp/leftpad foo 5
  foo
```

Take, for example, running background tasks in a web app. In a traditional architecture, you would have a set of task workers and a message queue to pass work from the web frontends to the task workers.

If your web frontends have access to a Swarm, you can run the task directly on your Swarm:

```python
client.run("tasks/reticulate-splines", detach=True)
```

You can run these from within other Docker applications

Take, for example, running background tasks in a web application. These are things continuously running that need managing, scaling, and so on.

However, if we wrapped up our background task inside a container and our web frontends had access to a Swarm, it could just run the task as a container on Swarm. This eliminates the need for two complex constantly running servers, and because it is run on-demand, it essentially auto-scales and makes efficient use of resources.

## Reading

 - [blog post coming soon]
 - [Introducing dexec](https://ahmetalpbalkan.com/blog/dexec/) – What if the Go os/exec library could containerize?

## Examples

 - https://github.com/bfirsh/serverless-docker-examples
 - Here is a good example i'm converting to a web api https://github.com/ahmetalpbalkan/go-dexec/tree/master/examples/600-parallel-compute

## Tools

 - [go-dcgi](https://github.com/bfirsh/go-dcgi) – CGI, but with Docker containers

## Client libraries

 - [docker-py](https://github.com/docker/docker-py) – Run Docker containers from Python apps
 - [dockerrun](https://github.com/bfirsh/dockerrun) – A simpler interface for running Docker containers in Python (soon to be part of docker-py)
 - [go-dexec](https://github.com/ahmetalpbalkan/go-dexec) – Like Go os/exec package but for Docker
 - [dockerode](https://github.com/apocas/dockerode) – Run Docker containers from Node.js apps
 - [docker-java](https://github.com/docker-java/docker-java) – Run Docker containers from Java apps

## Stuff that needs working on

We need your help!

 - A proxy that scopes a Docker API so that containers can securely manage and run "child" containers.
 - Helpers for injecting the Docker API socket into containers that are run.
