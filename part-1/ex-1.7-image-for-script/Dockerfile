FROM ubuntu:22.04 

WORKDIR /usr/src/app

RUN apt update -y && apt install curl -y

COPY script.sh .

CMD ./script.sh
