FROM ubuntu:latest

# Обновляем пакеты и устанавливаем необходимое ПО
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    python3-venv \
    wget \
    curl \
    iputils-ping \
    net-tools \
    dnsutils \
    iproute2 \
    traceroute \
    telnet \
    vim \
    openssh-server \
    sudo \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Создаем символическую ссылку для python -> python3
RUN ln -sf /usr/bin/python3 /usr/bin/python \
    && ln -sf /usr/bin/pip3 /usr/bin/pip

# Проверяем установку
RUN python --version && pip --version

# Создаем пользователя для ansible
RUN useradd -m -s /bin/bash ansible \
    && echo "ansible:ansible" | chpasswd \
    && echo "ansible ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Настройка SSH
RUN mkdir /var/run/sshd \
    && echo 'root:root' | chpasswd \
    && sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
