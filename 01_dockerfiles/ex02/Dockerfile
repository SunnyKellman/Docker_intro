# https://docs.docker.com/compose/rails/
# docker build -f Dockerfile -t ft-rails:on-build .
# docker build -f test.Dockerfile -t ex02 .
# docker run -it --name ft-rails_start -p 3000:3000 ex02

FROM ruby:latest

LABEL author=”skellman”

RUN apt-get update -y && apt-get install -y && apt-get install nodejs -y

# https://classic.yarnpkg.com/en/docs/install/#debian-stable <--- THIS
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -\
	&& echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
	&& apt-get update \
	&& apt-get install -y yarn
RUN gem install rails bundler

# Get to the right workdirectory and use rails to make the app
ONBUILD WORKDIR /opt
ONBUILD RUN rails new app
ONBUILD WORKDIR /opt/app

# Install and setup on ruby rails command
ONBUILD RUN bundler install
ONBUILD RUN rails db:migrate
ONBUILD RUN rails db:seed