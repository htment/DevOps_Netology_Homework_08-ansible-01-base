FROM centos:7

# Исправляем репозитории
RUN sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-* \
    && sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*

# Устанавливаем ПО
RUN yum install -y python3 openssh-server sudo && \
    yum clean all

# Генерируем SSH ключи
RUN ssh-keygen -A

# Настройка SSH
RUN echo 'root:root' | chpasswd && \
    sed -i 's/#PermitRootLogin yes/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
