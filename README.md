# วิดีโอบันทึกการอบรม React NodeJS Docker Workshop Online

### เอกสารประกอบการอบรม

- <https://bit.ly/reactnodedocker>

---

# ⚡ Day 1

[![Final video of fixing issues in your code in VS Code](https://i.ytimg.com/vi/SEtX6bPmIAg/maxresdefault.jpg)](https://www.youtube.com/SEtX6bPmIAg)

<details>
<summary> 👉 การขึ้นโปรเจ็กต์ React + Vite + TS + SWC:</summary>

▶️ Step 1: คำสั่งขึ้นโปรเจ็กต์

```bash
npm create vite@latest
```

▶️ Step 2: ตั้งชื่อโปรเจ็กต์ และเลือกรูปแบบเป็น typescript + swc

```bash
Project name >> sample-react

Select a framework >> React

Select a variant >> TypeScript + SWC
```

▶️ Step 2: เปิดเข้า VSCode

```bash
 code sample-react -r
```

▶️ Step 4: ติดตั้ง Node dependencies

```bash
 npm install
```

▶️ Step 5: รันโปรเจ็กต์ด้วย Vite

```bash
npm run dev
```

</details>

<details>
 <summary > 👉 การขึ้นโปรเจ็กต์ React + Vite + TS + SWC + Docker</summary>
<br/>

▶️ Step 1: คำสั่งขึ้นโปรเจ็กต์

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
version: "3.9"

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
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react-swc";

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
  },
});
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

- <https://github.com/iamsamitdev/react-layout-online>

👉 Note และ Script ที่ใช้สอน

- <https://github.com/iamsamitdev/react-layout-online/blob/main/NoteScriptReactNodeJSDockerDay2.txt>

---

# ⚡ Day 3 : React Material UI

### เอกสารประกอบการอบรม

- <https://github.com/iamsamitdev/react-mui-strapi-day3>

---

<details>
<summary> 👉 การขึ้นโปรเจ็กต์ React + Vite + TS + SWC+ Material UI:</summary>
<br/>

▶️ Step 1: Clone Project

```bash
git clone https://github.com/iamsamitdev/react-mui-strapi.git
```

▶️ Step 2: ตรวจสอบความถูกต้องของ docker-compose.yml ไฟล์

```bash
docker compose config
```

▶️ Step 3: Create container

```bash
docker compose up -d
docker compose up -d --build
```

▶️ Step 4: Install Material UI Library

```bash
npm install @mui/material @emotion/react @emotion/styled
```

▶️ Step 5: Config tsconfig.json

```json
"compilerOptions": {
    "lib": ["es6", "dom"],
    "noImplicitAny": true,
    "noImplicitThis": true,
    "strictNullChecks": true,
}
```

▶️ Step 6: ทดสอบเรียกใช้งาน MUI ที่ไฟล์ src/App.tsx

> ⚠️ ลบไฟล์ App.css ใน src อออกApples
>
> ⚠️ ลบคำสั่ง css ในไฟล์ index.css ออกทั้งหมด

```ts
import { Button } from "@mui/material";

function App() {
  return (
    <>
      <h1>MUI Button</h1>
      <Button variant="text">Text</Button>
      <Button variant="contained">Contained</Button>
      <Button variant="outlined">Outlined</Button>
    </>
  );
}

export default App;
```

>⚠️ เพิ่ม goole font ที่ไฟล์ index.html

```html
<link
  href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Thai:wght@200;300;400;500;600;700&display=swap"
  rel="stylesheet"
/>
```

> ⚠️ กำหนดโค้ดที่ไฟล์ index.css

```css
html,
body {
  font-family: "IBM Plex Sans Thai", sans-serif;
}
```

▶️ Step 7: ติดตั้ง Material Icons

```bash
npm install @mui/icons-material
```

▶️ Step 8: ทดสอบใช้งาน Icons

```html
 <h3>MUI Button with Icon</h3>
 <Stack direction="row" spacing={2}>
   <Button variant="text" startIcon={<Delete />}>Delete</Button>
   <Button variant="contained" startIcon={<Send />}>Send</Button>
   <Button variant="outlined" startIcon={<Photo />}>Photo</Button>
 </Stack> 
```

▶️ Step 9: การสร้าง Theme ใน MUI
>⚠️ สร้าง src/config/theme.ts

```ts
import { createTheme } from '@mui/material/styles'
import { green, grey, indigo } from '@mui/material/colors'

// Create a theme instance.
let theme = createTheme()

// Custom theme
theme = createTheme(theme, {
    palette: {
        primary: {
            main: grey[700],
            light: grey[50],
            dark: grey[900],
        },
        secondary: {
            main: indigo[50],
        },
        success: {
            main: green[500],
            light: green[50],
            dark: green[900],
        },
    },
    typography: {
        link: {
            fontSize: '0.8rem',
            [theme.breakpoints.up('md')]: {
                fontSize: '0.9rem',
            },
            fontWeight: 500,
            color: theme.palette.primary.main,
            display: 'block',
            cursor: 'pointer'
        },
        cardTitle: {
            fontSize: '1.2rem',
            display: 'block',
            fontWeight: 500
        },
        h6: {
            fontSize: '1rem',
        },
        h7: {
            fontSize: '0.8rem', 
        },
        h8: {
            fontSize: '0.7rem', 
        }
    },
})

export default theme
```

</details>
```

# ⚡ Day 4 : Strapi CMS Rest API

### เอกสารประกอบการอบรม

- <https://github.com/iamsamitdev/react-mui-strapi-day4>

---

<details>
<summary> 👉 การขึ้นโปรเจ็กต์ Node Strapi CMS Rest API:</summary>
<br/>

▶️ Step 1: Create brand new Strapi V4 Project

```bash
npx create-strapi-app@latest strapiapp --quickstart
```

▶️ Step 2: Create Dockerfile in strapiapp/Dockerfile

```bash

FROM node:18.16.0-alpine

# Install dependencies
# RUN apt-get update && apt-get install libvips-dev -y

# Node Environment
ARG NODE_ENV=development
ENV NODE_ENV=${NODE_ENV}

# Working Directory
WORKDIR /opt/

# Copy Files
COPY ./package*.json ./

# Path: strapiapp\Dockerfile
ENV PATH /opt/node_modules/.bin:$PATH

# Install Dependencies
RUN npm install

# Install MySQL Client
RUN npm install mysql --save

# Working Directory for production
WORKDIR /opt/app

# Copy Files for Strapi production
COPY . .

# Build Strapi
RUN npm run build

# Expose port
EXPOSE 1337

# Start Strapi
CMD ["npm", "run", "develop"]

```

▶️ Step 3: Config .dockerignore

```bash

**/.cache

**/.tmp

```

▶️ Step 4: ทดสอบ Build ตัว Dockerfile เป็น Image ดูก่อน

```bash

docker build -t mystrapi:latest .

```

▶️ Step 6: Create docker-compose.yml

```bash

version: '3.9'

# Network
networks:
  web_network:
    name: react_mui_strapi_network
    driver: bridge

# Services
services:

  # React App Development
  react_dev:
    build:
      context: ./reactapp
      dockerfile: Dockerfile.dev
    container_name: reactmui_dev
    restart: always
    volumes:
      - ./reactapp:/usr/app
      - /usr/app/node_modules  # Bookmarks Volume
    ports:
      - 5173:5173
    environment:
      - CHOKIDAR_USEPOLLING=true
    networks:
      - web_network

  # React App Production
  react_prod:
    build:
      context: ./reactapp
      dockerfile: Dockerfile.prod
    container_name: reactmui_prod
    restart: always
    ports:
      - 4173:4173
    networks:
      - web_network

  # Nginx Web Server
  nginx:
    image: nginx:latest
    container_name: nginx_reactmui
    restart: always
    ports:
      - 8800:80
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
    depends_on:
      - react_prod
    networks:
      - web_network

  # MySQL Database
  mysqldb:
    image: mysql:8.0.26
    container_name: mysql_reactmui
    restart: always
    ports:
      - 4406:3306
    command: mysqld --default-authentication-plugin=mysql_native_password
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: strapi
      MYSQL_USER: strapi
      MYSQL_PASSWORD: strapi
    volumes:
      - ./mysqldb:/var/lib/mysql
    networks:
      - web_network

  # Strapi CMS
  strapi:
    container_name: strapi_reactmui
    build: ./strapiapp
    image: mystrapi:latest
    restart: unless-stopped
    env_file: .env
    ports:
      - 1337:1337
    environment:
      DATABASE_CLIENT: ${DATABASE_CLIENT}
      DATABASE_HOST: mysqldb
      DATABASE_NAME: ${DATABASE_NAME}
      DATABASE_USERNAME: ${DATABASE_USERNAME}
      DATABASE_PORT: ${DATABASE_PORT}
      JWT_SECRET: ${JWT_SECRET}
      ADMIN_JWT_SECRET: ${ADMIN_JWT_SECRET}
      DATABASE_PASSWORD: ${DATABASE_PASSWORD}
      NODE_ENV: ${NODE_ENV}
    volumes:
      - ./strapiapp/config:/opt/app/config
      - ./strapiapp/src:/opt/app/src
      - ./strapiapp/package.json:/opt/package.json
      - ./strapiapp/.env:/opt/app/.env
    depends_on:
      - mysqldb
    networks:
      - web_network

```
