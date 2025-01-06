# Electron 快速入门

> [Electron 官网](https://www.electronjs.org/)

## 01. Electron快速入门

1. 使用以下命令初始化项目：

   ```bash
   npm init -y
   ```

2. 安装 Electron：

   ```bash
   npm install --save-dev electron
   ```

3. 修改 `package.json` 文件，添加启动脚本：

   ```json
   {
     "scripts": {
       "start": "electron ."
     }
   }
   ```

4. 创建 `index.html` 和 `index.js` 文件：

   - `index.html`:

     ```html
     <!DOCTYPE html>
     <html>
       <head>
         <title>My Electron App</title>
       </head>
       <body>
         <h1>Hello, Electron!</h1>
       </body>
     </html>
     ```

   - `index.js`:

     ```javascript
     // 引入 Electron 模块中的 app 和 BrowserWindow
     const { app, BrowserWindow } = require('electron');

     // 声明主窗口变量
     let mainWindow;

     // 当 Electron 初始化完成时触发 ready 事件
     app.on('ready', () => {
       // 创建一个新的浏览器窗口
       mainWindow = new BrowserWindow({
         width: 800, // 设置窗口宽度
         height: 600, // 设置窗口高度
         webPreferences: {
           nodeIntegration: true // 允许在渲染进程中使用 Node.js API
         }
       });

       // 加载本地的 HTML 文件到窗口中
       mainWindow.loadFile('index.html');
     });

     // 当所有窗口关闭时触发 window-all-closed 事件
     app.on('window-all-closed', () => {
       // 如果不是 macOS 平台，则退出应用
       if (process.platform !== 'darwin') {
         app.quit();
       }
     });

     // 当应用被激活（例如单击 Dock 图标）时触发 activate 事件
     app.on('activate', () => {
       // 如果没有打开的窗口，则重新创建一个窗口
       if (BrowserWindow.getAllWindows().length === 0) {
         mainWindow = new BrowserWindow({
           width: 800,
           height: 600,
           webPreferences: {
             nodeIntegration: true
           }
         });

         mainWindow.loadFile('index.html');
       }
     });
     ```
