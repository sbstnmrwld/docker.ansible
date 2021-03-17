FROM alpine:3.13@sha256:a75afd8b57e7f34e4dad8d65e2c7ba2e1975c795ce1ee22fa34f8cf46f96a3be

LABEL maintainer="seb@meerw.de" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.build-date=$BUILD_DATE \
    org.label-schema.vcs-ref=$VCS_REF \
    org.label-schema.name="sbstnmrwld/ansible" \
    org.label-schema.description="Ansible inside Docker" \
    org.label-schema.url="https://github.com/sbstnmrwld/docker.ansible" \
    org.label-schema.vcs-url="https://github.com/sbstnmrwld/docker.ansible" \
    org.label-schema.vendor="sbstnmrwld"

ENV PATH="/root/.cargo/bin:${PATH}"

RUN apk --no-cache add sudo python3 py3-pip openssl ca-certificates sshpass openssh-client rsync git curl && \
    apk --no-cache add --virtual build-dependencies python3-dev libffi-dev openssl-dev build-base && \
    curl https://static.rust-lang.org/rustup/dist/x86_64-unknown-linux-musl/rustup-init --output /tmp/rustup-init && chmod +x /tmp/rustup-init && /tmp/rustup-init -y && \
    pip3 install --no-cache-dir --upgrade pip cffi && \
    pip3 install --no-cache-dir ansible==2.10.3 && \
    pip3 install --no-cache-dir mitogen ansible-lint jmespath && \
    pip3 install --no-cache-dir --upgrade pywinrm && \
    rustup self uninstall -y && \
    apk del build-dependencies && rm -rf /var/cache/apk/*

RUN mkdir -p /etc/ansible && \
    echo 'localhost' > /etc/ansible/hosts

WORKDIR /ansible

CMD [ "ansible-playbook", "--version" ]
