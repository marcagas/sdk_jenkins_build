FROM ubuntu
MAINTAINER Marc Agas <marc.agas@cheetahdigital.com>

USER root
RUN apt-get update
RUN apt-get install -y build-essential
RUN apt-get install -y curl
RUN apt-get install -y vim
RUN apt-get install -y gnupg

ENV NODE_VERSION=10.10.0
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash \
	&& . $HOME/.nvm/nvm.sh \
	&& nvm install $NODE_VERSION \
	&& nvm alias default $NODE_VERSION \
	&& nvm use default \
	&& . ~/.bashrc \
	&& npm install gulp-cli -g \
	&& npm install gulp -D \
	&& npm install yarn -g

CMD echo 'done ....' 
