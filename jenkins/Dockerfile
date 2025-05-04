FROM jenkins/jenkins:lts

# ติดตั้ง Docker ใน Jenkins
USER root
RUN apt-get update && apt-get install -y docker.io

# ให้ Jenkins สามารถใช้ Docker ได้
# RUN usermod -aG docker jenkins

# USER jenkins