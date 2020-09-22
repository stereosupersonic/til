# docker compose 

https://docs.docker.com/engine/reference/builder/

## syntax
FROM [--platform=<platform>] <image> [AS <name>]

ENV <key> <value>
ENV <key>=<value> ...

ADD [--chown=<user>:<group>] <src>... <dest> # The ADD instruction copies new files, directories or remote file URLs from <src> and adds them to the filesystem of the image at the path <dest>.

COPY [--chown=<user>:<group>] <src>... <dest> # The COPY instruction copies new files or directories from <src> and adds them to the filesystem of the container at the path <dest>.

EXPOSE <port> [<port>/<protocol>...] The EXPOSE instruction informs Docker that the container listens on the specified network ports at runtime. You can specify whether the port listens on TCP or UDP, and the default is TCP if the protocol is not specified.

RUN executes command(s) in a new layer and creates a new image. E.g., it is often used for installing software packages.

CMD sets default command and/or parameters, which can be overwritten from command line when docker container runs.
      
ENTRYPOINT configures a container that will run as an executable.

...
