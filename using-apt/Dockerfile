FROM ubuntu:18.04

RUN apt update
RUN apt -y upgrade 

RUN apt install -y curl
RUN apt install -y wget
RUN apt install -y tar

# For ifconfig
RUN apt install -y net-tools

# For pyenv & python
RUN apt install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
    xz-utils tk-dev





##### Tools


### Git 
RUN apt install -y git
RUN git config --global user.email ""
RUN git config --global user.name "Arturo Avilés"

### ZSH http://ohmyz.sh/
RUN apt install zsh
RUN sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
# Add these lines to .bashrc
# export SHELL=/bin/zsh
# exec /bin/zsh -l

### VS Code https://code.visualstudio.com/docs/setup/linux
RUN curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg && \
    mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
RUN sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'

### Docker https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce-1
RUN apt update && \
    apt install apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
RUN apt-key fingerprint 0EBFCD88
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

RUN apt update && \
    apt install docker-ce

RUN docker run hello-world

### Kubernetes (kubectl) https://kubernetes.io/docs/tasks/tools/install-kubectl/
RUN apt update && apt install -y apt-transport-https
RUN curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
RUN cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
RUN deb http://apt.kubernetes.io/ kubernetes-xenial main && EOF
RUN apt update
RUN apt install -y kubectl

# Add Kubectl Autocompletion
RUN echo "source <(kubectl completion bash)" >> ~/.bashrc






##### Programming Languages Envs

### Anyenv https://github.com/riywo/anyenv
RUN git clone https://github.com/riywo/anyenv ~/.anyenv
RUN echo 'export PATH="$HOME/.anyenv/bin:$PATH"' >> ~/.zshenv
RUN echo 'eval "$(anyenv init -)"' >> ~/.zshenv
RUN exec $SHELL -l

### Pyenv
RUN anyenv install pyenv
## Get Virtualenv
RUN git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv
RUN echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc

### Rbenv
RUN anyenv install rbenv

### Node Nbenv
RUN anyenv install ndenv

### Goenv
RUN anyenv install goenv

### Phpenv
RUN anyenv install phpenv





##### Databases

### Redis
RUN apt install redis-tools
RUN apt install redis
# Turn on: sudo systemctl enable redis-server
# Turn off: sudo systemctl disable redis-server
# Run: redis-cli

### Mongodb https://linuxconfig.org/how-to-install-latest-mongodb-on-ubuntu-18-04-bionic-beaver-linux



### Mysql

## Client
RUN apt install mysql-client
# How to connect to external client: mysql -u USERNAME -p PASSWORD -h HOST-OR-SERVER-IP

## Server
RUN apt install mysql-server
# Secure installation
RUN sudo mysql_secure_installation




##### Cloud CLI's

### Google Cloud https://cloud.google.com/sdk/docs/quickstart-debian-ubuntu?hl=es
# Create environment variable for correct distribution
RUN export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)"
# Add the Cloud SDK distribution URI as a package source
RUN echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
# Import the Google Cloud Platform public key
RUN curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
# Update the package list and install the Cloud SDK
RUN apt update && apt install google-cloud-sdk
# Remember to run: gcloud init


### IBM Cloud 

## Cloudfoundry https://docs.cloudfoundry.org/cf-cli/install-go-cli.html
RUN wget -q -O - https://packages.cloudfoundry.org/debian/cli.cloudfoundry.org.key | sudo apt-key add -
RUN echo "deb https://packages.cloudfoundry.org/debian stable main" | sudo tee /etc/apt/sources.list.d/cloudfoundry-cli.list
RUN apt update
RUN apt install cf-cli

## Bx https://console.bluemix.net/docs/cli/reference/bluemix_cli/get_started.html#getting-started (Use OS Graphic Interface)
## Github: https://github.com/IBM-Cloud/ibm-cloud-cli-release
RUN wget https://clis.ng.bluemix.net/download/bluemix-cli/latest/linux64


### AWS https://aws.amazon.com/cli/
RUN pip install awscli


### Azure https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest
## https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt?view=azure-cli-latest
RUN AZ_REPO=$(lsb_release -cs)
RUN echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    tee /etc/apt/sources.list.d/azure-cli.list
RUN apt-key adv --keyserver packages.microsoft.com --recv-keys 52E16F86FEE04B979B07E28DB02C46DF417A0893
RUN curl -L https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
RUN apt install apt-transport-https
RUN apt update && sudo apt-get install azure-cli
# Run az login






##### Other

############################################################### STILL NOT READY
### Google Chrome https://www.google.com/chrome/
# Also check https://askubuntu.com/questions/845534/this-command-can-only-be-used-by-root
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' && \
    apt-get update && \
    apt-get install google-chrome-stable -y && \
    rm -rf /etc/apt/sources.list.d/google.list
# Check Google Chrome Version
RUN google-chrome-stable --version

### Postman https://blog.bluematador.com/posts/postman-how-to-install-on-ubuntu-1604/?utm_source=hootsuite&utm_medium=twitter&utm_campaign=
# https://www.getpostman.com/apps

### Spotify (Ubuntu Software)

### Dropbox (Ubuntu Software)


