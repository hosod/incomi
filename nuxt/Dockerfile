FROM node:12.5.0-alpine

ENV LANG C.UTF-8 && \
ENV TZ Asia/Tokyo

# system update
# RUN apt-get update && \
#     apt-get install -y vim less

WORKDIR /root

# install yarn command.
# - https://yarnpkg.com/lang/ja/docs/install/#alternatives-stable
# - https://github.com/yarnpkg/yarn/releases
ARG CMD_YARN_VERSION=1.13.0
RUN npm install --global yarn@$CMD_YARN_VERSION && \
    chmod +x /usr/local/bin/yarn

# install direnv command.
# - https://github.com/direnv/direnv
# - https://github.com/direnv/direnv/releases
ARG DEV_DIRENV_VERSION=v2.19.0
RUN wget -O direnv https://github.com/direnv/direnv/releases/download/$DEV_DIRENV_VERSION/direnv.linux-amd64 && \
    mv direnv /usr/local/bin/ && \
    chmod +x /usr/local/bin/direnv && \
    echo 'eval "$(direnv hook bash)"' >> ~/.bashrc

# install vue-cli
RUN npm install --global @vue/cli @vue/cli-init

# copy application code from host.
ADD src /src
WORKDIR /src/app


## install packages.
RUN yarn install

EXPOSE 3000
ENV HOST 0.0.0.0
CMD ["yarn", "run", "dev"]