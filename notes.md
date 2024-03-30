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
 
* docker run -v /path/on/host:/path/in/container [...] image
* docker run --mount type=bind,source="${PWD}",target=/app -it ubuntu bash 	
* -p 3456:8080 map the port 3456 to 8080



