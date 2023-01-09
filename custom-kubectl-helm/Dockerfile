FROM alpine/helm
RUN apk update
RUN apk --no-cache add git
RUN apk --no-cache add curl
ENV PYTHONUNBUFFERED=1
RUN apk add --update --no-cache python3 && ln -sf python3 /usr/bin/python
RUN python3 -m ensurepip
RUN pip3 install --no-cache --upgrade pip setuptools
RUN pip3 install awscli
RUN curl -LO https://dl.k8s.io/release/v1.24.0/bin/linux/amd64/kubectl \
    && mv kubectl /bin/kubectl \
    && chmod a+x /bin/kubectl
RUN VERSION=$(curl --silent "https://api.github.com/repos/argoproj/argo-cd/releases/latest" | grep '"tag_name"' | sed -E 's/.*"([^"]+)".*/\1/')
RUN curl -sSL -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/v2.2.25/download/argocd-linux-amd64
RUN chmod +x /usr/local/bin/argocd