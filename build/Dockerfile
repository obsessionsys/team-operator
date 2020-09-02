FROM quay.io/operator-framework/ansible-operator:v0.15.2

RUN set -ex && \
    curl -s -L https://storage.googleapis.com/kubernetes-release/release/v1.18.0/bin/linux/amd64/kubectl -o ${HOME}/kubectl && \
    chmod 755 ${HOME}/kubectl

COPY roles/ ${HOME}/roles/
COPY watches.yaml ${HOME}/watches.yaml

# RUN echo "gather_subset = !all" >> /etc/ansible/ansible.cfg