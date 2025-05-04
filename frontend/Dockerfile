# ใช้ Node.js เป็น base image
FROM node:18-alpine

# กำหนด working directory
WORKDIR /app

# คัดลอก package.json และ package-lock.json เพื่อทำการติดตั้ง dependencies
COPY package.json package-lock.json ./
RUN npm install

# คัดลอกโค้ดทั้งหมดเข้าไปใน container
COPY . .

# ตั้งค่าพอร์ตสำหรับ Vite (5173)
EXPOSE 5173

# คอมไพล์โปรเจกต์ (ถ้าต้องการ build static files)
RUN npm run build

# คำสั่งเริ่มต้นให้รัน Vite Dev Server
CMD ["npm", "run", "dev", "--", "--host"]