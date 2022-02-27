FROM arm64v8/ubuntu:20.04
SHELL ["/bin/bash", "--login", "-c"]
RUN DEBIAN_FRONTEND=noninteractive apt-get -y update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    git wget curl build-essential python3.8-full vim tmux tree unzip jq tig && \
    python3 -m venv /root/chalice-cdk; \
    source /root/chalice-cdk/bin/activate; \
    /root/chalice-cdk/bin/python3 -m pip install chalice==1.26.6; \
    /root/chalice-cdk/bin/python3 -m pip install chalice[cdk]==1.26.6;\
    /root/chalice-cdk/bin/python3 -m pip install httpie awscli==1.22.63 boto3==1.21.8;\
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash && \
    source /root/.bashrc; npm install -g npm; nvm install 'lts/*'; \
    npm install -g aws-cdk@2.14.0 && \
    echo source /root/chalice-cdk/bin/activate >>  /root/.bashrc && \
    rm -rf /var/lib/apt/lists/*
ENTRYPOINT /bin/bash
