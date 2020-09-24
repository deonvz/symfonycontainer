
# FROM is to define in which image this docker will be based on, in our case I’ll use the latest build from Ubuntu
FROM debian:stretch
#FROM nginx:alpine
# RUN is used to execute command inside the docker
RUN apt-get -y update
RUN apt-get -y install -y nginx vim nano
# COPY will copy a specific file from the host to the docker
COPY nginx.conf /etc/nginx/nginx.conf
# ADD will copy a specific folder from the host to the docker
ADD sites-enabled /etc/nginx/sites-enabled
RUN rm /etc/nginx/sites-enabled/default
# WORKDIR is used to define the base folder inside the docker
WORKDIR /var/www/public
# EXPOSE defines the ports that will be available to connect from the host to the guest
EXPOSE 80
EXPOSE 443
# CMD is responsible for executing a command/command- Start nginx
CMD ["nginx"]