FROM jenkins/jenkins:lts

USER root

# ติดตั้ง Docker
RUN apt-get update && apt-get install -y docker.io

# ให้ jenkins ใช้ docker ได้ (เพิ่มเข้ากลุ่ม docker และตรวจว่า docker.sock ถูก mount)
RUN usermod -aG docker jenkins

# ให้ shell ที่ Jenkins ใช้ reload group ใหม่
RUN echo "jenkins ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

USER jenkins
