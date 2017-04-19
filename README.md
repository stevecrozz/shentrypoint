# Shentrypoint

Shentrypoint is a script that provides an easy way to debug your Docker
applications without getting in your way. Shentrypoint does run as PID 1, but
it doesn't aim to be a full init process.

## Guiding Principles

1. When your container starts, your application should start
2. When your application dies, your container should die
3. When you send control signals to your container, your application process
   should receive them
4. When you send SIGINT (CTRL+C) to your container, you should get a shell
   prompt (not a stopped container) as if you'd been running your application
   process in the foreground from a shell all along
   
## Why?

We put together a lot of automation around running containers in terms
of configuration for inputs, network, volumes, etc, not to mention
connecting these containers to other systems in a deployment. Sometimes,
the easiest way to get a debugging environment is to take over an
existing container. Shentrypoint makes it possible to `docker attach` to
an existing container and you can pretend you had launched the
application as a foreground process all along. You can hit CTRL+C,
modify your container's filesystem, run arbitrary commands, restart your
application and debug it interactively.


## How to Use It

1. Create a [Procfile](https://devcenter.heroku.com/articles/procfile) where
   the keys are the command words you want to run later
2. Add shentrypoint to your docker image
3. Add `ENTRYPOINT /path/to/shentrypoint` to your Dockerfile

Use the command words defined in your Procfile to run your containers
