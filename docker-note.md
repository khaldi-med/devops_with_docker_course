### Docker is a set of platform as a service (PaaS) products that use OS-level virtualization to deliver software in packages called containers.

* DevOps is a development methodology aimed at bridging the gap between Development and Operations, emphasizing communication and collaboration, continuous integration, quality assurance and delivery with automated deployment utilizing a set of development practices.
 So stripping the jargon we get two definitions:
	1. Docker is a set of tools to deliver software in containers.
	2. Containers are packages of software.

* "works on my machine" problem for the software that works in locale machine and doesn't on the server".
   List all your images with "docker image ls".

### Container

* containers only contain that which is required to execute an application; and you can start, stop, and interact with them. They are isolated environments in the host machine with the ability to interact with each other and the host machine itself via defined methods (TCP/UDP).

* docker image rm <imageid>.

* If you have hundreds of stopped containers and you wish to delete them all, you should use: `docker container prune`.

* You can also use the image pull command to download images without running them: `docker image pull hello-world`.

* We should first stop the container using "docker container stop <image>", and then use "rm".

* We can use "docker container rm --force <iamgename>".

```
docker run -it ubuntu

-i (interactive)
-t (tty)
```
> The format is -p <host_port>:<container_port>

* The public key can be moved to the remote server with the command `scp` for example, which allows copying files between two distinct systems (cp was for copying inside the local system). 

	* `scp path/to/copyable/file user@palvelmen.osoite:path/to/target/folder`

* Docker containers were first developed on Linux for Linux.

* Containers are only possible due to the fact that the Linux OS provides some primitives, such as namespaces, control groups, layer capabilities, and more, all of which are leveraged in a very specific way by the container runtime and the Docker engine. Linux kernel namespaces, such as process ID (pid) namespaces or network (net) namespaces, allow Docker to encapsulate or sandbox processes that run inside the container. Control Groups make sure that containers cannot suffer from the noisy-neighbor syndrome, where a single application running in a container can consume most or all of the available resources of the whole Docker host. Control Groups allow Docker to limit the resources, such as CPU time or the amount of RAM, that each container is allocated.

* Due to the fact that container images are immutable, it is easy to have them scanned for common vulnerabilities and exposures (CVEs), and in doing so, increase the overall security of our applications.

* Another way to make our software supply chain more secure is to have our containers use a content trust. A content trust basically ensures that the author of a container image is who they pretend to be and that the consumer of the container image has a guarantee that the image has not been tampered with in transit. The latter is known as a man-in-the-middle (MITM) attack.

```
docker kill
docker rm 
docker rm --force <container>
```
* start process with -it and add --rm in order to remove it automatically after it has exited. 

* The --rm ensures that there are no garbage containers left behind.

* `docker search <image>` By default, docker search will only search from Docker Hub, but to a search different registry, you can add the registry address before the search term, for example, `docker search quay.io/hello`

* `docker diff`
* `docker build . -t <name>`
* `docker container ls -a --last 3`
* `Note also that -v creates a directory if the file does not exist.`

#### Volumes

* Docker volumes come in three types: **anonymous, named, and host-mounted.**

* In addition to Docker volumes, there are other ways to manage data in Docker, such as bind mounts. Bind mounts are directories on the host machine that are mounted into a container, similar to host-mounted volumes. However, bind mounts do not create a new layer, which means changes made in the container are reflected on the host machine and vice versa.
 
* docker run -v /path/on/host:/path/in/container [...] image
* docker run --mount type=bind,source="${PWD}",target=/app -it ubuntu bash 	
* docker run -p 3456:8080 map the port 3456 to 8080

* We could also limit connections to a certain protocol only, e.g. UDP by adding the protocol at the end: EXPOSE <port>/udp and -p <host-port>:<container-port>/udp.

``` 
* Running several connected containers typically refers to creating a multi-container application where containers communicate with each other. 
These containers can communicate with each other using Docker's internal networking. 
Docker-compose offers a streamlined method for orchestrating multiple containers using a docker-compose.yml file. 
However, containers can also be connected manually by creating custom Docker networks and then attaching containers to these networks. 
Once on the same network, containers can communicate using container names as hostnames. 
Manual connection offers detailed control but might be time-consuming with many containers, making tools like docker-compose preferred for more complex setups.

Connecting containers manually
Manually connecting containers in Docker refers to the process of setting up communication between multiple Docker containers without using Docker compose, When we run containers manually, we often use Docker's native networking capabilities to connect containers.

Let's use a sample example with a web application and a database.

Step 1: Create a custom Docker network.

> docker network create mynetwork

Step 2: Start a PostgreSQL container.

- docker run -d --network=mynetwork --name mydb -e \
  POSTGRES_PASSWORD=mysecretpassword postgres

Step 3: Start a web application container that connects to the PostgreSQL database.

Imagine you have an application that uses environment variables to connect to the database.

You would run:

docker run -d --network=mynetwork --name myapp -e DATABASE_HOST=mydb \
  -e DATABASE_PASSWORD=mysecretpassword myapp-image

Your application should use DATABASE_HOST as the hostname to connect to the PostgreSQL database.
```

* Sharing volumes between containers:
```
To share data between containers, you can use Docker volumes. Volumes are storage units that exist independently of containers, you create a volume and then mount this volume into multiple containers, This approach ensures data persistence and consistency across containers.

Let's take an example where you have two containers that need to access the same configuration files or need to share data.

Step 1: Create a Docker volume

docker volume create sharedvol

Step 2: Start a MySQL container and mount the shared volume for data persistence.

docker run -d --name mysql-container -v sharedvol:/var/lib/mysql mysql

Step 3: Start the WordPress container and mount the same volume to access the MySQL database data.

docker run -d --name wordpress-container -v sharedvol:/var/www/html wordpress

In this scenario, both the MySQL and WordPress containers will be able to access and modify data in the sharedvol volume, which is crucial for applications that require shared or persistent data.
```

* Adding containers to an existing network:
```
If you forgot to add a container to a network at startup, you can still attach it to the network later. First, identify the network using docker network ls. Then use the docker network connect command to attach the running container to the desired network.

* Step 1: Connect the container to the existing network.

> docker network connect mynetwork nginx-container

* Step 2: Verify the connection.

> docker container inspect nginx-container

Here, nginx-container is added to mynetwork, allowing to communicate with other containers on the same network.
```

* Running a container in the host network:
```
Running a Docker container in the host network means bypassing the virtual networking provided by Docker and using the host's networking directly.

Step1. Start an Nginx container in the host network

docker run --net=host -d --name nginx-host-container nginx

This command runs an Nginx container directly on the host's network stack. While this method provides performance benefits and easier port mapping, it also poses security risks as the container has unrestricted access to the host network. It can lead to port conflicts and potential exposure of the host system to security vulnerabilities. Therefore, it's crucial to assess the risks and benefits before opting for this setup.
```

### Part-2

* Docker Compose is a tool to deploy and manage multi-container applications.

* The "docker-compose.yml" file contains all the dependencies and configurations of the whole application stack.

* By using the **docker compose up** command, all the containers can be spun up.

* Docker Compose eliminates the need to manually configure each service on every device.

* Docker Compose can be used to deploy or manage both simple and complex applications.

* It saves time and resources by eliminating the need for manual configuration.

  - Example 

```
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8020:80"
    volumes:
      - ./web:/usr/share/nginx/html
    db:
      image: postgres
      environment:
        POSTGRES_USER: admin
        POSTGRES_PASSWORD: admin
        POSTGRES_DB: test_db
    app:
      image: my-custom-website
      environment:
        DATABASE_URL: postgres://admin:admin@db:4321/test_db
        depends_on:
          - db
```

#### Yaml

* YAML is a recursive acronym for YAML Ain't Markup Language. It's a human-readable data serialization standard for all programming languages. It is commonly used for configuration files and for storing and transferring data.The usual extensions for YAML files are .yaml and .yml.

* One may add comments to the YAML file. Comments start with # and go till newline. They can be made anywhere in the line, for example:
```
# The comment
metadata:  # this is metadata
```

### Volumes

* Docker volumes are a handy way to save data created by containers. You can save data in Docker volumes even after the containers are gone. This is useful for applications that require data persistence, such as databases or file servers. You can easily share data between containers by using Docker volumes, making it easier to develop, test, and deploy applications.

> docker volume create mydata
> docker run -d --name container2 -v mydata:/data busybox sleep 3600
> docker exec -it container2 sh
> cat /data/shared.txt
> exit

* 




























