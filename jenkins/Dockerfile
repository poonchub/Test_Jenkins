FROM jenkins/jenkins:lts

# ติดตั้ง Docker ใน Jenkins
USER root
RUN apt-get update && \
    apt-get install -y docker.io && \
    usermod -aG docker jenkins

# ให้ Jenkins สามารถใช้ Docker ได้
RUN chmod 666 /var/run/docker.sock

USER jenkins