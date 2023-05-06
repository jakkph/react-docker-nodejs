# วิดีโอบันทึกการอบรม React NodeJS Docker Workshop Online

  ### เอกสารประกอบการอบรม
  - https://bit.ly/reactnodedocker
---


# ⚡ Day 1

[![Final video of fixing issues in your code in VS Code](https://i.ytimg.com/vi/SEtX6bPmIAg/maxresdefault.jpg)](https://www.youtube.com/SEtX6bPmIAg)
 
<details>
<summary> 👉 การขึ้นโปรเจ็กต์ React + Vite + TS + SWC:</summary>

 🔸Step 1:  คำสั่งขึ้นโปรเจ็กต์

```bash
npm create vite@latest
```

 🔸Step 2: ตั้งชื่อโปรเจ็กต์ และเลือกรูปแบบเป็น typescript + swc

```bash
Project name >> sample-react

Select a framework >> React

Select a variant >> TypeScript + SWC
```

 🔸Step 3: เปิดเข้า VSCode

```bash
 code sample-react -r
```

 🔸Step 4: ติดตั้ง Node dependencies

```bash
 npm install
```

 🔸Step 5: รันโปรเจ็กต์ด้วย Vite

```bash
npm run dev
```

</details>

<details>
 <summary > 👉 การขึ้นโปรเจ็กต์ React + Vite + TS + SWC + Docker</summary>
<br/>

  ▶️ Step 1:  คำสั่งขึ้นโปรเจ็กต์

```bash
npm create vite@latest
```

  ▶️ Step 2: ตั้งชื่อโปรเจ็กต์ และเลือกรูปแบบเป็น typescript + swc

```bash
Project name >> sample-react-vite-docker

Select a framework >> React

Select a variant >> TypeScript + SWC
```

  ▶️ Step 3: เปิดเข้า VSCode

```bash
code sample-react-vite-docker -r
```

  ▶️ Step 4: เปิด Docker Desktop บนเครื่องขึ้นมา ทดสอบ HelloWorld Docker ดู

```bash
docker run hello-world
```

  ▶️ Step 5: สร้าง Dockerfile สำหรับกำหนด script ให้ docker ทำงานกับ image ที่ได้มา

```yml
# Pull the base image
FROM node:18.16.0-alpine

# Set the working directory
WORKDIR /usr/app

# Copy app dependencies to container
COPY ./package*.json ./

# Install dependencies
RUN npm install

# Copy code from host to container
COPY . .

# Expose Port
EXPOSE 5173

# Deploy app for local development
CMD [ "npm","run","dev" ]
```

  ▶️ Step 6: การสร้าง Container NodeJS+React ด้วยไฟล์ script ที่เรียกว่า docker-compose.yml

```yml
version: '3.9'

# Network
networks:
  web_network:
    name: reactdockervite
    driver: bridge

# React App Service
services:
  reactapp:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: reactapp_vite
    restart: always
    volumes:
      - ./:/usr/app
      - /usr/app/node_modules
    ports:
      - 5173:5173
    environment:
      - CHOKIDAR_USEPOLLING=true
    networks:
      - web_network
```

  ▶️ Step 7: แก้ไขไฟล์ vite.config.js

```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react-swc'

// <https://vitejs.dev/config/>
export default defineConfig({
  plugins: [react()],
  server: {
    watch: {
      usePolling: true,
    },
    host: true,
    strictPort: true,
    port: 5173,
  }
})
```

  ▶️ Step 8: ทดสอบว่าไฟล์ docker-compose.yml ทำงานถูกต้องหรือเปล่า

```bash
docker compose config
```

  ▶️ Step 9: ทำการ Run เป็น Service และ Container

```bash
docker compose up -d

# ถ้าแก้ไขอะไรใน dockerfile และ docker-compose.yml แล้วจะรันใหม่
docker compose up -d  --build
```

</details>

--- 

# ⚡ Day 2

[![Final video of fixing issues in your code in VS Code](https://i.ytimg.com/vi/H9FaJ0w5w08/maxresdefault.jpg)](https://youtu.be/H9FaJ0w5w08)

👉 ตัวอย่างโค๊ดโปรเจ็กต์ในคลิปนี้ 
  - https://github.com/iamsamitdev/react-layout-online

👉 Note และ Script ที่ใช้สอน 
  - https://github.com/iamsamitdev/react-layout-online/blob/main/NoteScriptReactNodeJSDockerDay2.txt
