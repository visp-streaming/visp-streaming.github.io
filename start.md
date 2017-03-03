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

Let's start with the infrastructure host. This is the machine where the RabbitMQ, MySQL and Redis services will be executed. Therefore you need to run a docker host, where you can execute the following commands.

`--net="host"` makes sure that the runtime has direct access to the containers via their ports

### Start Redis
```
docker run --net="host" -d --name redis -p 6379:6379 redis
```

### Start RabbitMQ
```
docker run --net="host" -d --name rabbitmq -e RABBITMQ_DEFAULT_USER=visp -e RABBITMQ_DEFAULT_PASS=visp -p 15672:15672 -p 5672:5672 rabbitmq:3-management
```


### Start MySQL
```
docker run --net="host" -d --name mysql -e MYSQL_ROOT_PASSWORD=visp -e MYSQL_DATABASE=visp -p 3306:3306 mysql
```

# Running via a docker container

```
docker run --net="host" -e "VISP_RUNTIME_IP=128.130.172.222" -e "VISP_IP=127.0.0.1" -e "VISP_INFRASTRUCTUREHOST=127.0.0.1" -e "SPRING_RABBITMQ_HOST=127.0.0.1" -e "SPRING_REDIS_HOST=127.0.0.1" -e "SPRING_DATASOURCE_URL=jdbc:mysql://127.0.0.1:3306/visp?verifyServerCertificate=false&useSSL=false&requireSSL=false" -d --name vispruntime bknasmueller/runtime
```

Setting the IPs correctly is critical: `VISP_RUNTIME_IP` is the public IP of the VISP runtime. This is also the IP that is used in the configuration file to distinguish different runtimes. In practise, it is the IP of the OpenStack instance where the above command is executed. `VISP_IP`: TODO: maybe we don't actually need it. All the other IPs must be set to `127.0.0.1` if deployment is done via docker on OpenStack. The reasons is that OpenStack instances cannot access themselves by their own public IPs (at least in our version).


In order to generate a docker container for the runtime, use this maven command (important: make sure to correctly set the credentials.properties before pushing):

```
mvn clean package docker:build -DpushImage -Dmaven.test.skip=true
```


# Topology Upload

Here are two example topology files: <a href="./files/scenario1.txt">scenario1</a> and <a href="./files/scenario2.txt">scenario2</a>.

Importantly, the IP addresses of the VISP runtimes need to be adjusted. In both cases, the operators are deployed on different runtimes to show how to specify such a behavior.


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
