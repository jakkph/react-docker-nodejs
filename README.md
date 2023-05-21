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

---

<br/>

<br/>

---

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

```tsx
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

<br/>

<br/>

# ⚡ Day 2

[![Final video of fixing issues in your code in VS Code](https://i.ytimg.com/vi/H9FaJ0w5w08/maxresdefault.jpg)](https://youtu.be/H9FaJ0w5w08)

👉 ตัวอย่างโค๊ดโปรเจ็กต์ในคลิปนี้

- <https://github.com/iamsamitdev/react-layout-online>

👉 Note และ Script ที่ใช้สอน

- <https://github.com/iamsamitdev/react-layout-online/blob/main/NoteScriptReactNodeJSDockerDay2.txt>

---

<br/>

<br/>

# ⚡ Day 3 : React Material UI

### Gighub : <https://github.com/iamsamitdev/react-mui-strapi-day3>

[![Final video of fixing issues in your code in VS Code](https://i.ytimg.com/vi/1Wj9pUspvBQ/maxresdefault.jpg)](https://youtu.be/1Wj9pUspvBQ)

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

```tsx
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

```tsx
 <h3>MUI Button with Icon</h3>
 <Stack direction="row" spacing={2}>
   <Button variant="text" startIcon={<Delete />}>Delete</Button>
   <Button variant="contained" startIcon={<Send />}>Send</Button>
   <Button variant="outlined" startIcon={<Photo />}>Photo</Button>
 </Stack> 
```

▶️ Step 9: การสร้าง Theme ใน MUI

```tsx
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



▶️ Step 10: config ไฟล์ main.tsx

```tsx
import React from 'react'
import ReactDOM from 'react-dom/client'

// ThemeProvider is required for Material-UI
import { ThemeProvider } from '@mui/material'

// Import the theme
import theme from './config/theme'

import App from './App.tsx'
import './index.css'

ReactDOM.createRoot(document.getElementById('root') as HTMLElement).render(
  <React.StrictMode>
    <ThemeProvider theme={theme}>
    <App />
    </ThemeProvider>
  </React.StrictMode>,
)
```

▶️ Step 11: Create AuthLayout.tsx in src/layouts

```bash
import { Outlet } from "react-router-dom"
import { Box } from "@mui/material"

const AuthLayout = () => {
  return (
    <>
      <Box>
        <Outlet />
      </Box>
    </>
  )
}

export default AuthLayout
```

▶️ Step 12: Install react-pro-sidebar

```bash
npm i react-pro-sidebar@1.0.0
```

▶️ Step 13: Create AppHeader.tsx in components

```tsx
import { AppBar, Box, IconButton, Toolbar } from "@mui/material"
import MenuIcon from '@mui/icons-material/Menu'
import SettingsIcon from '@mui/icons-material/Settings'
import LogoutIcon from '@mui/icons-material/Logout'

const AppHeader = () => {

    return (
        <AppBar position="sticky" sx={styles.appBar}>
            <Toolbar>
                <IconButton color="secondary">
                    <MenuIcon />
                </IconButton>
                <Box
                    component={'img'}
                    sx={styles.appLogo}
                    src="/assets/logo_round.png" />
                <Box sx={{ flexGrow: 1 }} />
                <IconButton title="Settings" color="secondary">
                    <SettingsIcon />
                </IconButton>
                <IconButton title="Sign Out" color="secondary">
                    <LogoutIcon />
                </IconButton>
            </Toolbar>
        </AppBar>
    )
}

const styles = {
    appBar: {
        // bgcolor: 'neutral.main'
        bgcolor: 'teal'
    },
    appLogo: {
        borderRadius: 2,
        width: 40,
        marginLeft: 2,
        cursor: 'pointer'
    }
}

export default AppHeader
```

▶️ Step 14: Create SideNav.tsx in src/components

```tsx
import { Avatar, Box, Typography } from "@mui/material"
import { Menu, MenuItem, Sidebar } from "react-pro-sidebar"
import DashboardOutlinedIcon from '@mui/icons-material/DashboardOutlined'
import StyleOutlinedIcon from '@mui/icons-material/StyleOutlined'
import SourceOutlinedIcon from '@mui/icons-material/SourceOutlined'
import AnalyticsOutlinedIcon from '@mui/icons-material/AnalyticsOutlined'

const SideNav = () => {
    return (
        <Sidebar
            style={{ height: "100%", top: 'auto' }}
            breakPoint="md"
            backgroundColor={'white'}
        >
            <Box sx={styles.avatarContainer}>
                <Avatar sx={styles.avatar} alt="Masoud" src="/assets/samit.jpg" />
                <Typography variant="body2" sx={styles.yourChannel}>Samit Koyom</Typography>
                <Typography variant="body2">Administrator</Typography>
            </Box>

            <Menu
                menuItemStyles={{

                }}>
                <MenuItem icon={<DashboardOutlinedIcon />}> <Typography variant="body2">Dashboard</Typography> </MenuItem>
                <MenuItem icon={<SourceOutlinedIcon />}> <Typography variant="body2">Product </Typography></MenuItem>
                <MenuItem icon={<AnalyticsOutlinedIcon />}> <Typography variant="body2">Report </Typography></MenuItem>
                <MenuItem icon={<StyleOutlinedIcon />}> <Typography variant="body2">Setting </Typography></MenuItem >
            </Menu >
        </Sidebar >
    )
}

const styles = {
    avatarContainer: {
        display: "flex",
        alignItems: "center",
        flexDirection: 'column',
        my: 5
    },
    avatar: {
        width: '40%',
        height: 'auto'
    },
    yourChannel: {
        mt: 1
    }
}

export default SideNav
```

▶️ Step 15: Create BackendLayout.tsx in src/layouts

```tsx
import { Outlet } from "react-router-dom"
import { Box } from "@mui/material"
import CssBaseline from "@mui/material/CssBaseline"
import AppHeader from "../components/AppHeader"
import SideNav from "../components/SideNav"

const BackendLayout = () => {
  return (
    <>
        <CssBaseline />
        <AppHeader />
        <Box sx={styles.container}>
          <SideNav />
          <Box component={"main"} sx={styles.mainSection}>
            <Outlet />
          </Box>
        </Box>
    </>
  )
}

const styles = {
  container: {
    display: "flex",
    bgcolor: "neutral.light",
  },
  mainSection: {
    px: 4,
    width: "100%",
    height: "100%",
    overflow: "auto",
  },
}

export default BackendLayout
```

▶️ Step 16: Create Login.tsx in src/pages

```ts
const Login = () => {
  return (
    <>
        <h1>Login</h1>
    </>
  )
}

export default Login
```

▶️ Step 17: Create Dashboard.tsx in src/pages

```ts
const Dashboard = () => {
  return (
    <>
        <h1>Dashboard</h1>
    </>
  )
}

export default Dashboard
```

▶️ Step 18: install react-router-dom

```ts
npm install react-router-dom@6
```
▶️ Step 19: config ProSidebarProvider in main.tsx

```ts
// Import ProSidebarProvider
import { ProSidebarProvider } from 'react-pro-sidebar'

ReactDOM.createRoot(document.getElementById('root') as HTMLElement).render(
  <React.StrictMode>
    <ProSidebarProvider>
      <ThemeProvider theme={theme}>
        <App />
      </ThemeProvider>
    </ProSidebarProvider>
  </React.StrictMode>,
)
```

▶️ Step 20: กำหนด Routing ที่ไฟล์ App.tsx

```ts
import { BrowserRouter, Route, Routes } from 'react-router-dom'
import Login from './pages/Login'
import BackendLayout from './layouts/BackendLayout'
import AuthLayout from './layouts/AuthLayout'

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route element={<AuthLayout />}>
          <Route path="/" element={<Login />} />
        </Route>
        <Route element={<BackendLayout />}>
          <Route path="/backend/dashboard" element={<h1>Dashboard</h1>} />
        </Route>
      </Routes>
    </BrowserRouter>
  )
}

export default App
```

▶️ Step 21: Create Product.tsx, Report.tsx, Setting.tsx in src/pages

```ts

const Product = () => {
    return (
      <>
          <h1>Product</h1>
      </>
    )
  }
  
  export default Product
  ```

▶️ Step 22: Config Route in App.tsx

```ts

import { BrowserRouter, Route, Routes } from 'react-router-dom'
import Login from './pages/Login'
import BackendLayout from './layouts/BackendLayout'
import AuthLayout from './layouts/AuthLayout'

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route element={<AuthLayout />}>
          <Route path="/" element={<Login />} />
        </Route>
        <Route element={<BackendLayout />}>
          <Route path="/backend/dashboard" element={<h1>Dashboard</h1>} />
          <Route path="/backend/product" element={<h1>Product</h1>} />
          <Route path="/backend/report" element={<h1>Report</h1>} />
          <Route path="/backend/setting" element={<h1>Setting</h1>} />
        </Route>
      </Routes>
    </BrowserRouter>
  )
}

export default App
```

▶️ Step 23: Set Link in SideNav.tsx

```ts
<MenuItem component={<Link to="/backend/dashboard" />} icon={<DashboardOutlinedIcon />}> <Typography variant="body2">Dashboard</Typography> </MenuItem>
<MenuItem component={<Link to="/backend/product" />} icon={<SourceOutlinedIcon />}> <Typography variant="body2">Product </Typography></MenuItem>
<MenuItem component={<Link to="/backend/report" />} icon={<AnalyticsOutlinedIcon />}> <Typography variant="body2">Report </Typography></MenuItem>
<MenuItem component={<Link to="/backend/setting" />} icon={<StyleOutlinedIcon />}> <Typography variant="body2">Setting </Typography></MenuItem >
```

▶️ Step 24: Toggle SideNav

```ts
import { useProSidebar } from "react-pro-sidebar"

const AppHeader = () => {

// useProSidebar hook
  const { collapseSidebar, toggleSidebar, broken } = useProSidebar()

}

 <IconButton onClick={()=> broken ? toggleSidebar() : collapseSidebar()} color="secondary">
    <MenuIcon />
  </IconButton>
```

▶️ Step 25: Create Login Screen

```ts
import { TextField, Button } from "@mui/material"

const Login = () => {
  return (
    <>
        <h1>Login</h1>
        <form>
          <div>
            <TextField label="Username"
              type="text"
              variant="outlined"
            />
          </div>

          <div>
            <TextField label="Password"
              type="password"
              variant="outlined"
            />
          </div>
          <div>
            <Button variant="contained" color="primary" type="submit">
              Login
            </Button>
          </div>
        </form>
    </>
  )
}

export default Login
```

▶️ Step 26: การจัดการกับแบบฟอร์มด้วย react-hook-form

>⚠️ ติดตั้ง npm install react-hook-form@7 เรียกใช้งานที่หน้า Login.tsx

```ts
---
import { TextField, Button } from "@mui/material"
import { useForm } from "react-hook-form"

const Login = () => {

  // useForm hook
  const { register, handleSubmit, formState: { errors } } = useForm()

  // onSubmit function
  const onSubmit = (data: any) => {
    console.log(data)
  }

  return (
    <>
        <h1>Login</h1>
        <form onSubmit={handleSubmit(onSubmit)}>
          <div>
            <TextField label="Username"
              type="text"
              variant="outlined"
              {...register("username", { required: true, minLength: 5 })}
              error={errors.username ? true : false}
              helperText={errors.username ? "Username is required" : ""}
            />
          </div>

          <div>
            <TextField label="Password"
              type="password"
              variant="outlined"
              {...register("password", { required: true })}
              error={errors.password ? true : false}
              helperText={errors.password ? "Password is required" : ""}
            />
          </div>
          <div>
            <Button variant="contained" color="primary" type="submit">
              Login
            </Button>
          </div>
        </form>
    </>
  )
}

export default Login




</details>
```

# ⚡ Day 4 : Strapi CMS Rest API

### Gighub : <https://github.com/iamsamitdev/react-mui-strapi-day4>

---

▶️ Step 10: config ไฟล์ main.tsx

```tsx
import React from 'react'
import ReactDOM from 'react-dom/client'

// ThemeProvider is required for Material-UI
import { ThemeProvider } from '@mui/material'

// Import the theme
import theme from './config/theme'

import App from './App.tsx'
import './index.css'

ReactDOM.createRoot(document.getElementById('root') as HTMLElement).render(
  <React.StrictMode>
    <ThemeProvider theme={theme}>
    <App />
    </ThemeProvider>
  </React.StrictMode>,
)
```

▶️ Step 11: Create AuthLayout.tsx in src/layouts

```tsx
import { Outlet } from "react-router-dom"
import { Box } from "@mui/material"

const AuthLayout = () => {
  return (
    <>
      <Box>
        <Outlet />
      </Box>
    </>
  )
}

export default AuthLayout
```

▶️ Step 12: Install react-pro-sidebar

```bash
npm i react-pro-sidebar@1.0.0
```

▶️ Step 13: Create AppHeader.tsx in components

```tsx
import { AppBar, Box, IconButton, Toolbar } from "@mui/material"
import MenuIcon from '@mui/icons-material/Menu'
import SettingsIcon from '@mui/icons-material/Settings'
import LogoutIcon from '@mui/icons-material/Logout'

const AppHeader = () => {

    return (
        <AppBar position="sticky" sx={styles.appBar}>
            <Toolbar>
                <IconButton color="secondary">
                    <MenuIcon />
                </IconButton>
                <Box
                    component={'img'}
                    sx={styles.appLogo}
                    src="/assets/logo_round.png" />
                <Box sx={{ flexGrow: 1 }} />
                <IconButton title="Settings" color="secondary">
                    <SettingsIcon />
                </IconButton>
                <IconButton title="Sign Out" color="secondary">
                    <LogoutIcon />
                </IconButton>
            </Toolbar>
        </AppBar>
    )
}

const styles = {
    appBar: {
        // bgcolor: 'neutral.main'
        bgcolor: 'teal'
    },
    appLogo: {
        borderRadius: 2,
        width: 40,
        marginLeft: 2,
        cursor: 'pointer'
    }
}

export default AppHeader
```

▶️ Step 14: Create SideNav.tsx in src/components

```tsx
import { Avatar, Box, Typography } from "@mui/material"
import { Menu, MenuItem, Sidebar } from "react-pro-sidebar"
import DashboardOutlinedIcon from '@mui/icons-material/DashboardOutlined'
import StyleOutlinedIcon from '@mui/icons-material/StyleOutlined'
import SourceOutlinedIcon from '@mui/icons-material/SourceOutlined'
import AnalyticsOutlinedIcon from '@mui/icons-material/AnalyticsOutlined'

const SideNav = () => {
    return (
        <Sidebar
            style={{ height: "100%", top: 'auto' }}
            breakPoint="md"
            backgroundColor={'white'}
        >
            <Box sx={styles.avatarContainer}>
                <Avatar sx={styles.avatar} alt="Masoud" src="/assets/samit.jpg" />
                <Typography variant="body2" sx={styles.yourChannel}>Samit Koyom</Typography>
                <Typography variant="body2">Administrator</Typography>
            </Box>

            <Menu
                menuItemStyles={{

                }}>
                <MenuItem icon={<DashboardOutlinedIcon />}> <Typography variant="body2">Dashboard</Typography> </MenuItem>
                <MenuItem icon={<SourceOutlinedIcon />}> <Typography variant="body2">Product </Typography></MenuItem>
                <MenuItem icon={<AnalyticsOutlinedIcon />}> <Typography variant="body2">Report </Typography></MenuItem>
                <MenuItem icon={<StyleOutlinedIcon />}> <Typography variant="body2">Setting </Typography></MenuItem >
            </Menu >
        </Sidebar >
    )
}

const styles = {
    avatarContainer: {
        display: "flex",
        alignItems: "center",
        flexDirection: 'column',
        my: 5
    },
    avatar: {
        width: '40%',
        height: 'auto'
    },
    yourChannel: {
        mt: 1
    }
}

export default SideNav
```

▶️ Step 15: Create BackendLayout.tsx in src/layouts

```tsx
import { Outlet } from "react-router-dom"
import { Box } from "@mui/material"
import CssBaseline from "@mui/material/CssBaseline"
import AppHeader from "../components/AppHeader"
import SideNav from "../components/SideNav"

const BackendLayout = () => {
  return (
    <>
        <CssBaseline />
        <AppHeader />
        <Box sx={styles.container}>
          <SideNav />
          <Box component={"main"} sx={styles.mainSection}>
            <Outlet />
          </Box>
        </Box>
    </>
  )
}

const styles = {
  container: {
    display: "flex",
    bgcolor: "neutral.light",
  },
  mainSection: {
    px: 4,
    width: "100%",
    height: "100%",
    overflow: "auto",
  },
}

export default BackendLayout
```

▶️ Step 16: Create Login.tsx in src/pages

```tsx
const Login = () => {
  return (
    <>
        <h1>Login</h1>
    </>
  )
}

export default Login
```

▶️ Step 17: Create Dashboard.tsx in src/pages

```tsx
const Dashboard = () => {
  return (
    <>
        <h1>Dashboard</h1>
    </>
  )
}

export default Dashboard
```

▶️ Step 18: install react-router-dom

```bash
npm install react-router-dom@6
```

▶️ Step 19: config ProSidebarProvider in main.tsx

```tsx
// Import ProSidebarProvider
import { ProSidebarProvider } from 'react-pro-sidebar'

ReactDOM.createRoot(document.getElementById('root') as HTMLElement).render(
  <React.StrictMode>
    <ProSidebarProvider>
      <ThemeProvider theme={theme}>
        <App />
      </ThemeProvider>
    </ProSidebarProvider>
  </React.StrictMode>,
)
```

▶️ Step 20: กำหนด Routing ที่ไฟล์ App.tsx

```tsx
import { BrowserRouter, Route, Routes } from 'react-router-dom'
import Login from './pages/Login'
import BackendLayout from './layouts/BackendLayout'
import AuthLayout from './layouts/AuthLayout'

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route element={<AuthLayout />}>
          <Route path="/" element={<Login />} />
        </Route>
        <Route element={<BackendLayout />}>
          <Route path="/backend/dashboard" element={<h1>Dashboard</h1>} />
        </Route>
      </Routes>
    </BrowserRouter>
  )
}

export default App
```

▶️ Step 21: Create Product.tsx, Report.tsx, Setting.tsx in src/pages

```tsx
const Product = () => {
    return (
      <>
          <h1>Product</h1>
      </>
    )
  }
  
  export default Product
  ```

▶️ Step 22: Config Route in App.tsx

```tsx
import { BrowserRouter, Route, Routes } from 'react-router-dom'
import Login from './pages/Login'
import BackendLayout from './layouts/BackendLayout'
import AuthLayout from './layouts/AuthLayout'

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route element={<AuthLayout />}>
          <Route path="/" element={<Login />} />
        </Route>
        <Route element={<BackendLayout />}>
          <Route path="/backend/dashboard" element={<h1>Dashboard</h1>} />
          <Route path="/backend/product" element={<h1>Product</h1>} />
          <Route path="/backend/report" element={<h1>Report</h1>} />
          <Route path="/backend/setting" element={<h1>Setting</h1>} />
        </Route>
      </Routes>
    </BrowserRouter>
  )
}

export default App
```

▶️ Step 23: Set Link in SideNav.tsx

```tsx
<MenuItem component={<Link to="/backend/dashboard" />} icon={<DashboardOutlinedIcon />}> <Typography variant="body2">Dashboard</Typography> </MenuItem>
<MenuItem component={<Link to="/backend/product" />} icon={<SourceOutlinedIcon />}> <Typography variant="body2">Product </Typography></MenuItem>
<MenuItem component={<Link to="/backend/report" />} icon={<AnalyticsOutlinedIcon />}> <Typography variant="body2">Report </Typography></MenuItem>
<MenuItem component={<Link to="/backend/setting" />} icon={<StyleOutlinedIcon />}> <Typography variant="body2">Setting </Typography></MenuItem >
```

▶️ Step 24: Toggle SideNav

```tsx
import { useProSidebar } from "react-pro-sidebar"

const AppHeader = () => {

// useProSidebar hook
  const { collapseSidebar, toggleSidebar, broken } = useProSidebar()

}

 <IconButton onClick={()=> broken ? toggleSidebar() : collapseSidebar()} color="secondary">
    <MenuIcon />
  </IconButton>
```

▶️ Step 25: Create Login Screen

```tsx
import { TextField, Button } from "@mui/material"

const Login = () => {
  return (
    <>
        <h1>Login</h1>
        <form>
          <div>
            <TextField label="Username"
              type="text"
              variant="outlined"
            />
          </div>

          <div>
            <TextField label="Password"
              type="password"
              variant="outlined"
            />
          </div>
          <div>
            <Button variant="contained" color="primary" type="submit">
              Login
            </Button>
          </div>
        </form>
    </>
  )
}

export default Login
```

▶️ Step 26: การจัดการกับแบบฟอร์มด้วย react-hook-form

>⚠️ ติดตั้ง package เรียกใช้งานที่หน้า Login.tsx

```bash
npm install react-hook-form@7 
```

```tsx
import { TextField, Button } from "@mui/material"
import { useForm } from "react-hook-form"

const Login = () => {

  // useForm hook
  const { register, handleSubmit, formState: { errors } } = useForm()

  // onSubmit function
  const onSubmit = (data: any) => {
    console.log(data)
  }

  return (
    <>
        <h1>Login</h1>
        <form onSubmit={handleSubmit(onSubmit)}>
          <div>
            <TextField label="Username"
              type="text"
              variant="outlined"
              {...register("username", { required: true, minLength: 5 })}
              error={errors.username ? true : false}
              helperText={errors.username ? "Username is required" : ""}
            />
          </div>

          <div>
            <TextField label="Password"
              type="password"
              variant="outlined"
              {...register("password", { required: true })}
              error={errors.password ? true : false}
              helperText={errors.password ? "Password is required" : ""}
            />
          </div>
          <div>
            <Button variant="contained" color="primary" type="submit">
              Login
            </Button>
          </div>
        </form>
    </>
  )
}

export default Login
```
</details>

<br/>

<br/>

</details>

# ⚡ Day 4 : Strapi CMS Rest API

### Gighub : <https://github.com/iamsamitdev/react-mui-strapi-day4>

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
</details>
