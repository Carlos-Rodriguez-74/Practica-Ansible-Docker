
FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    openssh-server \
    sudo \
    python3 \
    python3-apt \
    && rm -rf /var/lib/apt/lists/*

RUN useradd -m -s /bin/bash ansible && \
    echo "ansible:ansible" | chpasswd && \
    usermod -aG sudo ansible && \
    echo "ansible ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/ansible && \
    chmod 0440 /etc/sudoers.d/ansible

RUN mkdir -p /run/sshd

RUN printf "PasswordAuthentication yes\nPermitRootLogin no\nUsePAM no\n" \
    > /etc/ssh/sshd_config.d/ansible.conf

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
