---
layout: quickstart
---

<section id="download-section" class="doc-section">
<h2 class="section-title">Download</h2>
<div class="section-block">
You can run VISP by downloading the source code from github: <br /><br />


<a class="btn btn-primary btn-cta" href="https://github.com/visp-streaming/runtime" target="_blank">
<i class="fa fa-cloud-download"></i> VISP Runtime</a>
<a class="btn btn-primary btn-cta" href="https://github.com/visp-streaming/processingNodes" target="_blank">
<i class="fa fa-cloud-download"></i> VISP Processing Nodes</a>

</div>
</section>

<section id="download-section" class="doc-section">
<h2 class="section-title">Infrastructure Host</h2>
<div class="section-block">
Let's start with the infrastructure host. This is the machine where the RabbitMQ, MySQL and Redis daemons will be executed.


</div>
</section>

<section id="download-section" class="doc-section">
<h2 class="section-title">Docker Host</h2>
<div class="section-block">
The docker host is the machine where the individual nodes' docker containers will be running.

</div>
</section>

## run redis
docker run -d --name redis -p 6379:6379 redis

## run rabbitmq image
docker run -d --hostname rabbitmq --name rabbitmq -e RABBITMQ_DEFAULT_USER=visp -e RABBITMQ_DEFAULT_PASS=visp -p 15672:15672 -p 5672:5672 rabbitmq:3-management

## run mysql image
docker run -d --name mysql -e MYSQL_ROOT_PASSWORD=visp -e MYSQL_DATABASE=visp -p 3306:3306 mysql



# Message Infrastructure
Start a RabbitMQ instance:

```
docker run -d --hostname rabbitmq --name rabbitmq -e RABBITMQ_DEFAULT_USER=visp -e RABBITMQ_DEFAULT_PASS=visp -p 15672:15672 -p 5672:5672 rabbitmq:3-management
```

Configure the properties:
```
spring.rabbitmq.host = dockerhost where the docker command was executed
```

# Shared Storage
Start a Redis instance on the same host as the RabbitMQ:
```
docker run -d --name redis -p 6379:6379 redis
```

# Data Backend
Start a Mysql instance on the same host as the RabbitMQ:
```
docker run -d --name mysql -e MYSQL_ROOT_PASSWORD=visp -e MYSQL_DATABASE=visp -p 3306:3306 mysql
```


# Configure the Dockerhost image
Set the id of an CoreOS image on an Openstack instance for the parameter *visp.dockerhost.image* in application.properties

# Access Configuration
Create a copy of the *credential.sample.properties* and store it as *credential.properties* and add the access credentials to this file.

# Start VISP runtime

The application can be started with:

```
mvn spring-boot:run

```

At startup, the VISP runtime creates the topology based on the configured topology (*visp.topology* in *application.propertie*s), starts an initial Dockerhost for the services and created the initial processing configuration (one instance for each service).

# Configuring the Runtime

## Topology selection
The topology can be choosen based on the value of *visp.topology*  in *application.properties*.

## BTU configuration of Hosts
The billing time unit of the Hosts can be configured based on the value of *visp.btu* in *application.properties*.

## Graceperiod for shutdown
The graceperiod for shutting down processing services can be set based on the value of *visp.shutdown.graceperiod* in *application.properties*.
