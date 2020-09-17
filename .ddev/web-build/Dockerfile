# Install and configure nvm
ARG BASE_IMAGE
FROM $BASE_IMAGE

ENV NVM_DIR=/usr/local/nvm
ENV NODE_DEFAULT_VERSION=v14.4.0

RUN curl -sL https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh -o install_nvm.sh
RUN mkdir -p $NVM_DIR && bash install_nvm.sh
RUN echo "source $NVM_DIR/nvm.sh" >>/etc/profile
RUN bash -ic "nvm install $NODE_DEFAULT_VERSION && nvm use $NODE_DEFAULT_VERSION"
RUN chmod -R ugo+w $NVM_DIR

RUN npm install gulp-cli -g

# Example of how to add other tools to an image.
# https://stackoverflow.com/questions/58415512/how-can-i-add-and-use-nvm-in-a-ddev-web-container/61934500#61934500
