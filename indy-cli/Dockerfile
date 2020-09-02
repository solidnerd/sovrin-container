FROM docker.io/library/ubuntu:bionic

RUN apt-get update
RUN apt-get install -y gpg software-properties-common wget pwgen
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys CE7709D068DB5E88
RUN add-apt-repository "deb https://repo.sovrin.org/sdk/deb bionic stable"

RUN apt-get update
RUN apt-get install -y indy-cli

RUN wget https://raw.githubusercontent.com/sovrin-foundation/sovrin/master/sovrin/pool_transactions_builder_genesis \
  && wget https://raw.githubusercontent.com/sovrin-foundation/sovrin/stable/sovrin/pool_transactions_sandbox_genesis \
  && wget https://raw.githubusercontent.com/sovrin-foundation/sovrin/stable/sovrin/pool_transactions_live_genesis

RUN mkdir -p /etc/indy-cli
COPY cliconfig.json /etc/indy-cli/cliconfig.json

COPY generate-keys.sh /usr/local/bin/generate-keys
RUN chmod +x /usr/local/bin/generate-keys

CMD ["indy-cli", "--config", "/etc/indy-cli/cliconfig.json"]