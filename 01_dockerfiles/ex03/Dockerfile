# https://medium.com/@1997corry/running-your-own-gitlab-on-docker-community-edition-39c4a8f99553
FROM debian:latest

LABEL author=”skellman”

RUN apt-get update && \
	apt-get upgrade -y && apt-get install -y dialog apt-utils && \
	apt-get install -y curl openssh-server ca-certificates postfix
	
RUN	curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash && \
	apt-get install -y gitlab-ce tzdata && \
	apt update && apt-get clean

# Making the container not stuck on these bad bois: grafana & prometheus. 
RUN sed -i "s/# grafana\['enable'\] = true/grafana['enable'] = false/g" /etc/gitlab/gitlab.rb
RUN sed -i "s/# prometheus_monitoring\['enable'\] = true/prometheus_monitoring\['enable'\] = false/g" /etc/gitlab/gitlab.rb

EXPOSE 22 80 443

ENTRYPOINT (/opt/gitlab/embedded/bin/runsvdir-start &) && gitlab-ctl reconfigure && tail -f /dev/null

# Build Image
# docker build -t ex03 .

# Create Container
# docker run --name ex03 -itd --shm-size=4g --restart=on-failure  -p 8080:80 -p 8022:22 -p 8443:443 --privileged ex03 && docker attach ex03

# From browser:
# 192.168.99.101:8080