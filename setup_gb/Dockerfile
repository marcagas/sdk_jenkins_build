FROM jenkinsci/jnlp-slave:3.26-1
MAINTAINER Marc Agas <marc.agas@cheetahdigital.com>

USER root
RUN apt-get update
RUN apt-get install -y build-essential
RUN apt-get install -y curl
RUN apt-get install -y vim
RUN apt-get install -y gnupg

ENV NODE_VERSION=10.10.0
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash \
	&& . $HOME/.nvm/nvm.sh \
	&& nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default

RUN apt-get install --assume-yes git

# installing yarn
#RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN apt-get install apt-transport-https
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -

RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y yarn

# Authorize SSH Host
RUN mkdir -p /root/.ssh && \
	chmod 0700 /root/.ssh && \
    ssh-keyscan github.com > /root/.ssh/known_hosts

COPY id_rsa /root/.ssh/

RUN git clone git@github.com:LoyalSphere/stellar-web-gb.git
RUN cd stellar-web-gb && yarn install

EXPOSE 8081

RUN echo "Starging yarn..."

CMD yarn run start