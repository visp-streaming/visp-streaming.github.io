---
layout: quickstart
---

<div id="toc"></div>


# Download

<div class="section-block">
You can run VISP by downloading the source code from github: <br /><br />

	<a class="btn btn-primary btn-cta" href="https://github.com/visp-streaming/runtime" target="_blank">
	<i class="fa fa-cloud-download"></i> VISP Runtime</a>
</div>


# Infrastructure Host

Let's start with the infrastructure host. This is the machine where the RabbitMQ, MySQL and Redis services will be executed. Therefore you need to run a docker host, where you can execute the following commands

### Start Redis
```
docker run -d --name redis -p 6379:6379 redis
```

### Start RabbitMQ
```
docker run -d --hostname rabbitmq --name rabbitmq -e RABBITMQ_DEFAULT_USER=visp -e RABBITMQ_DEFAULT_PASS=visp -p 15672:15672 -p 5672:5672 rabbitmq:3-management
```


### Start MySQL
```
docker run -d --name mysql -e MYSQL_ROOT_PASSWORD=visp -e MYSQL_DATABASE=visp -p 3306:3306 mysql
```

# Configuration

## application.properties

TBD

- visp.ip
- visp.infrastructurehost
- spring.rabbitmq.host
- spring.redis.host
- spring.datasource.url
- visp.dockerhost.image


## credential.properties

Create a copy of the *credential.sample.properties* and store it as *credential.properties* and add the access credentials to this file.


TBD

## Required Software

TBD: install maven + java

If you want to be able to view the current topology as an image of a directed graph, you need to have the "dot" application available at /usr/bin/dot". This can easily be installed in Ubuntu using the following command:

`apt-get install graphviz`



# Run VISP



```
mvn spring-boot:run

```

# Setup VISP

## Resource Pools

TBD

## Deploy Topology

TBD

# Data Provider

## Download

<div class="section-block">
You can run VISP by downloading the source code from github: <br /><br />

	<a class="btn btn-primary btn-cta" href="https://github.com/visp-streaming/dataProvider" target="_blank">
	<i class="fa fa-cloud-download"></i> VISP DataProvider</a>
</div>

## Run Data Provider

```
mvn spring-boot:run

```

## Stream Data

TBD


# Fine tuning

TBD: discuss all other attributes in application.properties as well as in the configuration menue


