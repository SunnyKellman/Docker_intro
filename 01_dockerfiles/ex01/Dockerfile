# Get TS3 version 3.1.1

FROM debian

LABEL author=”skellman”

EXPOSE 8897/udp 10011/tcp 30033/tcp

RUN DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y wget bzip2

RUN wget https://files.teamspeak-services.com/releases/server/3.12.1/teamspeak3-server_linux_amd64-3.12.1.tar.bz2

RUN tar xfvj teamspeak3-server_linux_amd64-3.12.1.tar.bz2
RUN mv teamspeak3-server_linux_amd64 /opt/teamspeak
RUN rm teamspeak3-server_linux_amd64-3.12.1.tar.bz2

ENV TS3SERVER_LICENSE accept
ADD entrypoint.sh /entrypoint.sh

#bash to let it execute
ENTRYPOINT ["bash","/entrypoint.sh"]

# docker build -t ex01 .
# docker run -it --name ts3 -p 9987:9987/udp -p 10011:10011 -p 30033:30033 --rm ex01