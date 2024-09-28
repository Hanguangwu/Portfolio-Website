# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

# 3D Portfolio Website 搭建

## 简介

Let's build a cool 3D website together! You'll learn how to make a portfolio with fun interactive parts, like a floating island and a fox that moves when you type. It'll allow you to show off your skills and get a job!

[原作者3d-portfolio](https://3d-portfolio.com/)

[Build and Deploy an Amazing 3D Developer Portfolio in React with Three.js-GitHub](https://github.com/adrianhajdin/3D_portfolio)

[部署到Render平台的Demo](https://portfolio-website-nt3f.onrender.com/)


## Time Stamps 👇
### 00:00:00 - Intro
### 00:06:35 - Setup

新建文件夹，进入执行`npm create vite@latest`

```

> npx
> create-vite

✔ Project name: … 3d_portfolio
✔ Select a framework: › React
✔ Select a variant: › JavaScript

Scaffolding project in /home/xxxxxxxx/3d_portfolio...

Done. Now run:

  cd 3d_portfolio
  npm install
  npm run dev
```


删除src文件夹再新建

安装tailwind css，搜索 vite 

https://tailwindcss.com/docs/guides/vite


```
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Configure your template paths

Add the paths to all of your template files in your tailwind.config.js file.

```css
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Add the Tailwind directives to your CSS

Add the @tailwind directives for each of Tailwind’s layers to your ./src/index.css file.

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

```
npm run dev

> 3d_portfolio@0.0.0 dev
> vite


  VITE v5.4.6  ready in 565 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h + enter to show help
```

安装`react-router-dom`执行`npm install react-router-dom`

此时App.jsx内容如下：

```jsx
import { Route, BrowserRouter as Router, Routes } from "react-router-dom";

// import { Footer, Navbar } from "./components";
// import { About, Contact, Home, Projects } from "./pages";

const App = () => {
  return (
    <main className='bg-slate-300/20'>
      <Router>
        {/* <Navbar /> */}
        <Routes>
          <Route path='/' element={<Home />} />
          <Route
            path='/*'
            element={
              <>
                <Routes>
                  <Route path='/about' element={About} />
                  <Route path='/projects' element={Projects } />
                  <Route path='/contact' element={Contact } />
                </Routes>
                {/* <Footer /> */}
              </>
            }
          />
        </Routes>
      </Router>
    </main>
  );
};

export default App;
```
### 00:18:58 - Navbar

新建components文件夹

安装VSCode插件`ES7 React/Redux/GraphQL/React-Native snippets`方便使用快捷键rafc、rafce等

在react.js相关代码中`import { logo } from "../assets/images";`这样可以调用一个名为logo.svg的图片吗？如果图片为`logo.png`，此时可以调用吗？

在React.js中，`import { logo } from "../assets/images";`这种方式只能导入SVG格式的图片文件。如果图片为PNG格式的`logo.png`，需要使用另一种方式进行导入，例如可以使用`import logo from "../assets/images/logo.png";`这样的方式来导入PNG格式的图片文件。

创建 index.js文件

已知如下的react代码：

```jsx
import { NavLink } from "react-router-dom";

// import { logo } from "../assets/images";

const Navbar = () => {
  return (
    <header className='header'>
      <NavLink to='/'>
        {/* <img src={logo} alt='logo' className='w-18 h-18 object-contain' /> */}
        What The Fuck 
      </NavLink>
      <nav className='flex text-lg gap-7 font-medium'>
        <NavLink to='/about' className={({ isActive }) => isActive ? "text-blue-600" : "text-black" }>
          About
        </NavLink>
        <NavLink to='/projects' className={({ isActive }) => isActive ? "text-blue-600" : "text-black"}>
          Projects
        </NavLink>
      </nav>
    </header>
  );
};

export default Navbar;
```

App.jsx

```jsx
import { Route, BrowserRouter as Router, Routes } from "react-router-dom";


import { Navbar } from "./components/Navbar";
// import { Footer, Navbar } from "./components";
import { About, Contact, Home, Projects } from "./pages";

const App = () => {
  return (
    <main className='bg-slate-300/20'>
      <Router>
        <Navbar />
        <Routes>
          <Route path='/' element={<Home />} />
          <Route
            path='/*'
            element={
              <>
                <Routes>
                  <Route path='/about' element={<About />} />
                  <Route path='/projects' element={<Projects />} />
                  <Route path='/contact' element={<Contact />} />
                </Routes>
                <Footer />
              </>
            }
          />
        </Routes>
      </Router>
    </main>
  );
};

export default App;
```

上面明明导出了Navbar为什么还会爆出如下的错误呢？错误信息如下：

```
Uncaught SyntaxError: The requested module '/src/components/Navbar.jsx?t=1726559808962' does not provide an export named 'Navbar' 
```

你要帮我找出问题并改正。

根据您提供的代码和错误信息，问题出在 `Navbar` 组件的导出方式。您在 `App.jsx` 中导入 `Navbar` 组件时使用了命名导入，但在 `Navbar.jsx` 中您使用的是默认导出。

解决方案

1. **修改 `Navbar.jsx` 的导出方式：**

   如果您希望使用命名导入，那么需要将 `Navbar` 组件的导出改为命名导出：

   ```jsx
   // Navbar.jsx
   import { NavLink } from "react-router-dom";

   export const Navbar = () => {
     return (
       <header className='header'>
         <NavLink to='/'>
           {/* <img src={logo} alt='logo' className='w-18 h-18 object-contain' /> */}
           What The Fuck 
         </NavLink>
         <nav className='flex text-lg gap-7 font-medium'>
           <NavLink to='/about' className={({ isActive }) => isActive ? "text-blue-600" : "text-black" }>
             About
           </NavLink>
           <NavLink to='/projects' className={({ isActive }) => isActive ? "text-blue-600" : "text-black"}>
             Projects
           </NavLink>
         </nav>
       </header>
     );
   };
   ```

2. **或者，保持默认导出并修改导入：**

   如果您希望保持默认导出，则需要在 `App.jsx` 中使用默认导入：

   ```jsx
   // App.jsx
   import Navbar from "./components/Navbar";  // 这里使用默认导入
   ```

总结

- **命名导出**：在 `Navbar.jsx` 中使用 `export const Navbar = ...`，并在 `App.jsx` 中使用 `{ Navbar }` 导入。
- **默认导出**：在 `Navbar.jsx` 中使用 `export default Navbar`，并在 `App.jsx` 中直接导入 `Navbar`。

选择一种方式并修正后，错误应该会消失。

### 00:25:17 - HomePage

安装`npm install @react-three/fiber`

安装`react-three/drei`执行`npm install @react-three/drei`

sketchfab 3D模型网站

Drag 'n' drop your GLTF file here or try it with Suzanne

https://gltf.pmnd.rs/


### 00:36:05 - Island

新建models文件夹添加Island.jsx文件

安装`npm install @react-spring/three`

修改 vite.config.js文件添加对`.glb`的包含


修改`.eslintrc.cjs`文件在`ignorePatterns`中增加`src`

### 00:48:26 - Sky


### 00:50:42 - Rotation, Bird & Plane


Bird Math.sin

### 01:27:19 - Popups

文字部分

```jsx
<div className='absolute top-28 left-0 right-0 z-10 flex items-center justify-center'>
        {currentStage && <HomeInfo currentStage={currentStage} />}
      </div>
```

### 01:36:40 - Contact

emailjs

安装`npm install @emailjs/browser`

### 01:44:14 - Email.JS

Send Email Directly From Your Code

No server code needed. Focus on things that matter!

https://www.emailjs.com/

200 requests left

emailjs 是一个用于发送电子邮件的 JavaScript 库，可以帮助开发者在网站或应用程序中轻松地发送电子邮件。 它提供了一个简单的 API 接口，可以发送邮件并处理邮件传输的细节。

要安装 emailjs，可以使用 npm 或 yarn 进行安装：

使用 npm：
```bash
npm install emailjs-com
```

使用 yarn：
```bash
yarn add emailjs-com
```

关于 `VITE_APP_EMAILJS_SERVICE_ID`，这是 emailjs 在 Vite 环境下可以使用的配置属性。这个值是 emailjs 提供的服务 ID，可以在 emailjs 官网上注册账号并创建一个邮件服务后获取。你可以在 emailjs 的控制台中找到你的服务 ID，并将其作为环境变量设置到你的项目中。 例如在 Vite 中可以通过添加在 `.env` 文件中添加如下内容来配置：

```
VITE_APP_EMAILJS_SERVICE_ID = YOUR_EMAILJS_SERVICE_ID
```

这样在项目中就可以通过 `import.meta.env.VITE_APP_EMAILJS_SERVICE_ID` 来获取这个值。

### 01:54:11 - Fox

创建useAlert

### 02:08:04 - Alert


### 02:13:34 - About Page


创建 constants 中的 index.js 包含技能清单

react-vertical-timeline-component

安装指令`npm i react-vertical-timeline-component`
### 02:30:32 - CTA

About最下面链接Contact

### 02:32:44 - Fix Plane and Keyboard handle


### 02:34:58 - Projects Page


### 02:44:35 - Adding Sound

修改 index.html 中基本信息
### 02:50:24 - Deployment

执行`npm run build`生成dist文件夹

https://www.hostinger.jp/

原作者部署在该平台上



