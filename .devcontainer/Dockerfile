FROM debian:stable-slim

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN apt update -y && \
    apt upgrade -y && \
    apt install -y \
    wget \
    sudo \
    net-tools \
    git

RUN wget https://sourceforge.net/projects/xampp/files/XAMPP%20Linux/8.2.12/xampp-linux-x64-8.2.12-0-installer.run/download -O xampp-installer.run && \
    chmod +x xampp-installer.run && \
    ./xampp-installer.run && \
    rm xampp-installer.run

RUN groupadd -f -g $USER_GID $USERNAME && \
    useradd -u $USER_UID -g $USER_GID -m $USERNAME && \
    echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME && \
    chmod 0440 /etc/sudoers.d/$USERNAME

RUN sed -i 's/Listen 80/Listen 8080/' /opt/lampp/etc/httpd.conf

EXPOSE 8080 3306

USER $USERNAME