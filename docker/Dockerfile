ARG BASE=quay.io/operator-framework/ansible-operator:v1.3.0
FROM ${BASE} 

ARG KUBECTL_VERSION=1.21.1

RUN set -ex && \
    curl -s -L https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl -o ${HOME}/kubectl && \
    chmod 755 ${HOME}/kubectl

COPY requirements.yml ${HOME}/requirements.yml
RUN ansible-galaxy collection install -r ${HOME}/requirements.yml \
 && chmod -R ug+rwx ${HOME}/.ansible
 
COPY roles/ ${HOME}/roles/
COPY watches.yaml ${HOME}/watches.yaml
